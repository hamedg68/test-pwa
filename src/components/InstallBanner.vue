<template>
  <div>
    <p>is mobile check : {{ isMobileCheck }}</p>
    <a-modal
      v-model:visible="visible"
      title="Basic Modal"
      @ok="handleOk"
      @cancel="visible = false"
    >
      <h4>آیا مایل به نصب بر روی تلفن همراه خود هستید؟</h4>
    </a-modal>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue";

const visible = ref<boolean>(false);
const isMobileCheck = ref<boolean>(false);

const handleOk = () => {
  installApp();
};

let differedPrompt: any = null;

function installApp() {
  visible.value = false;
  differedPrompt.prompt();
  differedPrompt.userChoice.then((choiceResult: any) => {
    if (choiceResult.outcome === "accepted") {
      console.log("user accepted the A2HS prompt");
    } else {
      console.log("user dismissed the A2HS prompt");
    }
    visible.value = false;
    differedPrompt = null;
  });
}

onMounted(() => {
  isMobileCheck.value = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);

  window.addEventListener("beforeinstallprompt", (e) => {
    e.preventDefault();
    differedPrompt = e;
    if (isMobileCheck.value) {
      visible.value = true;
    }
  });
});
</script>

<style></style>
