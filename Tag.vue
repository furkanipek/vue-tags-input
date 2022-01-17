<template>
  <span class="tag" :class="selectedTheme">
    <span class="content">{{ tag }}</span>
    <span class="close" @click="$emit('removeOneTagEvent', index)">X</span>
  </span>
</template>

<script>
export default {
  props: ["tag", "index", "tagColor"],
  data() {
    return {
      selectedTheme: null,
    };
  },
  created() {
    if (
      [
        "default",
        "success",
        "danger",
        "warning",
        "info",
        "primary",
        "secondary",
      ].indexOf(this.tagColor) != -1
    ) {
      this.selectedTheme = this.tagColor;
    } else {
      this.selectedTheme = "default";
    }
  },
};
</script>

<style scoped>
.default {
  background-color: #e2e3e5;
  border: 1px solid #d6d8db;
  color: #black;
}

.success {
  background-color: #d5eddb;
  border: 1px solid #c3e6cb;
  color: #155724;
}
.primary {
  background-color: #cce5ff;
  border: 1px solid #b8daff;
  color: #004085;
}
.secondary {
  background-color: #e2e3e5;
  border: 1px solid #d6d8db;
  color: #004085;
}
.info {
  background-color: #d1ecf1;
  border: 1px solid #bee5eb;
  color: #0c5460;
}
.warning {
  background-color: #fff3cd;
  border: 1px solid #ffeeba;
  color: #856404;
}
.danger {
  background-color: #f8d7da;
  border: 1px solid #f5c6cb;
  color: #721c24;
}

.tag {
  padding: 10px;
  cursor: default;
  font-size: 14px;
  margin-right: 10px;
  border-radius: 10px;
}
.tag * {
  font-size: 14px;
}
.tag .close {
  font-size: 12px;
  cursor: pointer;
}
</style>