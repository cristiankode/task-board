<script setup lang="ts">
import type { Task, ID } from "@/types";
const props = defineProps<{
  task: Task;
}>();

const emit = defineEmits<{
  (e: "delete", payload: string): void;
}>();
const focused = ref(false);
onKeyStroke("Backspace", (e) => {
  if(focused.value) emit("delete", props.task.id)
})
</script>
<template>
  <div
    :title="task.createdAt.toLocaleString()"
    class="task bg-white p-2 mb-2 rounded shadow-sm max-w-[250px] flex"
    @focus="focused = true"
    @blur="focused = false"
    tabindex="0"
  >
    <DragHandle class="pr-2" />
    <span>
      {{ task.title }}
      {{ task.createdAt.toLocaleDateString() }}
    </span>
  </div>
</template>