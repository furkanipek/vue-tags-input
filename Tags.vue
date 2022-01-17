<template>
  <div class="tag-container">
    <Tag
      v-for="(tag, index) in tags"
      :key="tag"
      :tag="tag"
      :index="index"
      :tagColor="color"
      @removeOneTagEvent="removeOneTag($event)"
    ></Tag>
    <input type="text" @keydown.enter="addTag" @keyup.backspace="removeTag" />
    <div class="error" v-if="error">Bu etiket daha önceden eklenmiş!!!</div>
  </div>
</template>

<script>
import Tag from "./Tag";
export default {
  props: {
    value: {
      required: false,
    },
    color: {
      type: String,
      required: false,
      default: "default",
    },
  },
  components: {
    Tag,
  },
  data() {
    return {
      tags: [],
      error: false,
    };
  },
  methods: {
    addTag(event) {
      let text = event.target;
      let matchedTag = false;
      if (text.value.length > 0) {
        this.tags.forEach((tag) => {
          if (tag.toLowerCase() === text.value.toLowerCase()) {
            matchedTag = true;
          }
        });
        if (matchedTag) {
          this.error = true;
          setTimeout(() => {
            this.error = false;
          }, 2000);
        } else {
          this.tags.push(text.value);
          text.value = "";
        }
      }
    },
    removeTag(event) {
      if (event.target.value.length <= 0) {
        let LastTag = this.tags.pop();
        if (LastTag !== undefined) {
          event.target.value = LastTag;
        }
      }
    },
    removeOneTag(index) {
      this.tags.splice(index, 1);
    },
  },
  created() {
    if (this.value) {
      if (this.value.length > 0) {
        this.tags = this.value.split(",");
      }
    }
  },
  watch: {
    tags() {
      this.$emit("input", this.tags.join(","));
    },
  },
};
</script>

<style scoped>
.tag-container {
  border: 1px solid #ccc;
  padding: 20px;
}

input {
  outline: none;
  height: 30px;
  width: 100px;
}

.error {
  font-size: 12px;
  color: red;
  margin-top: 5px;
}
</style>