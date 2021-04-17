<template>
  <tr>
    <td class="tdata">
      {{ id + 1 }}
    </td>
    <td class="tdata">
      {{ value.text }}
    </td>
    <td class="tdata">
      {{ value.credit }}
    </td>
    <td class="tdata">
      <input
        type="number"
        min="0"
        class="p-2 border rounded"
        placeholder="Баллни киритинг"
        v-model="pointTaken"
      />
    </td>
  </tr>
</template>

<script>
export default {
  props: ["totalCredits", "value", "id"],
  data() {
    return {
      pointTaken: null,
    };
  },
  watch: {
    pointTaken(point) {
      this.$emit("update:totalCredits", {
        ...this.totalCredits,
        [this.id]: point * this.value.credit,
      });
    },
  },
};
</script>

<style></style>
