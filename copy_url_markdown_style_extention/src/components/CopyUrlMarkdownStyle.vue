<template>
  <div class="main-content">
    <h1>Copy URL</h1>
    <p><b>status: </b>{{ copyStatus }}</p>
    <p><b>text: </b>{{ copyText }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

/* global chrome */

let copyStatus = ref("");
let copyText = ref("");

try {
  // console.log("callback");
  let [tab] = await chrome.tabs.query({
    active: true,
    lastFocusedWindow: true,
  });
  // console.log("after callback: ");
  // console.log(tab);

  let decodedUrl = decodeURI(tab.url);

  let str = getUrlAsMarkdown(decodedUrl, tab.title);

  copyClipBord(str);

  copyStatus.value = "successful!!";
  copyText.value = str;
} catch(e) {
  // console.log(e);
  copyStatus.value = "error";
}

function copyClipBord(textVal) {
  var copyFrom = document.createElement("textarea");
  copyFrom.textContent = textVal;

  var bodyElm = document.getElementsByTagName("body")[0];
  bodyElm.appendChild(copyFrom);

  copyFrom.select();
  var retVal = document.execCommand("copy");
  bodyElm.removeChild(copyFrom);
  return retVal;
}

function getUrlAsMarkdown(url, title) {
  return "[" + title + "](" + url + ")";
}
</script>

<style scoped>
.main-content {
  text-align: left;
}
</style>
