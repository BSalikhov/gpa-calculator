<template>
  <tr>
    <td width="10" class="whitespace-pre-wrap tdata">
      {{ id + 1 }}
    </td>
    <td class="whitespace-pre-wrap tdata">
      {{ value.text }}
    </td>
    <td class="whitespace-pre-wrap tdata">
      {{ value.credit }}
    </td>
    <td class="whitespace-pre-wrap tdata">
      <input
        type="number"
        min="0"
        class="w-16 p-2 border rounded md:mr-4 lg:w-auto"
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
