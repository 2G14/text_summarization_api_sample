<template lang="pug">
  div
    div
      form
        div
          Textarea(maxlength="200" v-model="text" @change="makeLinenumbers" placeholder="要約したいテキストを入力してください。")
        Select(label="言語" v-model="selectedLanguage" :options="languages" @change="makeLinenumbers")
        Select(label="要約後の文章数" v-model="selectedLinenumber" :options="linenumbers")
        div
          button(type="button" @click="request")
            | 要約
    List(:items="items")
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";
import Textarea from "./Textarea.vue";
import Select from "./Select.vue";
import List from "./List.vue";

@Component({
  components: {
    Textarea,
    Select,
    List
  }
})
export default class Content extends Vue {
  /** data */
  /**
   * text
   */
  private text: string = "";
  /**
   * selected language
   */
  private selectedLanguage: string = "ja";
  /**
   * languages
   */
  private languages: Array<{ label: string; value: string }> = [
    { label: "日本語", value: "ja" },
    { label: "英語", value: "en" }
  ];
  /**
   * selected linenumber
   */
  private selectedLinenumber: number = 1;
  /**
   * linenumber
   */
  private linenumbers: Array<{ label: number; value: number }> = [
    { label: 1, value: 1 }
  ];
  /**
   * result items
   */
  private items: string[] = [];
  /** methods */
  private makeLinenumbers(): void {
    this.linenumbers = [];
    const language = this.selectedLanguage;
    const text = this.text;
    const separation: string =
      (language === "ja" && "。") || (language === "en" && "\\.") || "";
    const count: number = (text.match(new RegExp(separation, "g")) || " ")
      .length;
    for (let i = 0; i < count - 1; i++)
      this.linenumbers.push({ label: i + 1, value: i + 1 });
    if (this.linenumbers.length === 0)
      this.linenumbers.push({ label: 1, value: 1 });
    this.selectedLinenumber = 1;
  }
  private request(): void {
    const key = process.env.VUE_APP_KEY;
    const formdata = new FormData();
    formdata.append("apikey", key);
    formdata.append("sentences", this.text);
    formdata.append("linenumber", this.selectedLinenumber.toString());
    formdata.append("separation", this.separation());
    fetch("https://api.a3rt.recruit-tech.co.jp/text_summarization/v1", {
      method: "POST",
      body: formdata
    })
      .then((response: Response) => response.json())
      .then((data: Data) => {
        console.log(data.status);
        if (data.status === 0) {
          const summaries = data.summary;
          this.items.unshift(
            summaries.join(this.separation()) + this.separation()
          );
          if (this.items.length > 10) this.items.pop();
        } else {
          errorHandle(data.status);
        }
      })
      .catch((error: Error) => console.error("Error: ", error));
  }
  private separation(): string {
    switch (this.selectedLanguage) {
      case "ja":
        return "。";
        break;
      case "en":
        return ".";
        break;
      default:
        return "";
        break;
    }
  }
}
interface Data {
  message: string;
  status: number;
  summary: string[];
}
function errorHandle(status: number) {
  let msg = "";
  switch (status) {
    case 1400:
      msg =
        "テキストは２文以上を入力してください。\n文章の最後には必ず日本語では「。」、英語では「.」を入力してください。";
      break;
    case 1413:
      msg = "テキストは200文字以下、10文章以下で入力してください。";
      break;
    case 1500:
      msg = "処理でエラーが発生しました。";
      break;
    default:
      break;
  }
  console.log(msg);
  alert(msg);
}
</script>

<style lang="sass" scoped>
div
  text-align: center
  div
    form
      div
        textarea
</style>
