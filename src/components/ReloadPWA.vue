<script setup lang="ts">
import { computed } from "@vue/reactivity";
import { useRegisterSW } from "virtual:pwa-register/vue";
import { ref, watch } from "vue";

// replaced dyanmicaly
const reloadSW: any = "__RELOAD_SW__";

const { offlineReady, needRefresh, updateServiceWorker } = useRegisterSW({
  immediate: true,
  onRegistered(r) {
    if (reloadSW === "true") {
      r &&
        setInterval(async () => {
          // eslint-disable-next-line no-console
          console.log("Checking for sw update");
          await r.update();
        }, 20000 /* 20s for testing purposes */);
    } else {
      // eslint-disable-next-line no-console
      console.log(`SW Registered: ${r}`);
    }
  },
});

const visible = ref<boolean>(false);
const handleOk = () => {
  if (needRefresh.value) {
    updateServiceWorker();
  } else {
    close();
  }
};
const close = async () => {
  offlineReady.value = false;
  needRefresh.value = false;
};

const modalTitle = computed(() => {
  return offlineReady.value
    ? "آفلاین"
    : needRefresh.value
    ? "به روز رسانی"
    : "";
});
const modalContent = computed(() => {
  return offlineReady.value
    ? "برنامه آماده کار به صورت آفلاین"
    : needRefresh.value
    ? "محتوای جدید در دسترس است. آیا میخواهید برنامه را به روز رسانی کنید؟"
    : "";
});
const modalBtnText = computed(() => {
  return offlineReady.value ? "خب" : needRefresh.value ? "تایید" : "";
});
const cancelBtnText = computed(() => {
  return offlineReady.value ? " " : needRefresh.value ? "لغو" : " ";
});

watch([offlineReady, needRefresh], () => {
  if (offlineReady.value || needRefresh.value) visible.value = true;
  else if (!offlineReady.value && !needRefresh.value) visible.value = false;
});

defineExpose({
  offlineReady,
  needRefresh,
});
</script>

<template>
  <div>
    offlineReady : {{ offlineReady }} **** needRefresh : {{ needRefresh }}
  </div>
  <a-modal
    v-model:visible="visible"
    :title="modalTitle"
    @ok="handleOk"
    :cancelText="cancelBtnText"
    :okText="modalBtnText"
    @cancel="close()"
  >
    <h4>{{ modalContent }}</h4>
  </a-modal>
</template>

<style></style>
