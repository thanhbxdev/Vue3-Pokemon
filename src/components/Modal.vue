<template>
  <div>
    <a-button type="primary" @click="showModal">Open Modal</a-button>
    <a-modal v-model:visible="visible" v-bind:title="title" @ok="handleOk">
      <p>{{ content }}</p>
    </a-modal>
  </div>
</template>

<script>
import {ref} from 'vue';

export default {
  name: "ModalAntd",
  props: {
    title: {
      type: String,
      required: true
    },
    content: {
      type: String,
      default: ""
    }
  },
  setup() {
    const visible = ref(false);

    const showModal = () => {
      visible.value = true;
    };

    const handleOk = () => {
      visible.value = false;
    };

    return {
      visible,
      showModal,
      handleOk,
    };
  },
}
</script>
