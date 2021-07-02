<template>
  <tr>
    <!-- <td width="10" class="whitespace-pre-wrap tdata">
      {{ id + 1 }}
    </td> -->
    <td class="whitespace-pre-wrap tdata w-48 lg:w-80">
      {{ id + 1 }}. {{ value.text }}
    </td>
    <td class="whitespace-pre-wrap tdata">
      {{ value.credit }}
    </td>
    <td class="whitespace-pre-wrap tdata w-20">
      <input
        type="number"
        min="0"
        class="w-16 mr-2 lg:mr-4 p-2 border rounded lg:w-auto"
        placeholder="Баллни киритинг"
        v-model="pointTaken"
      />
    </td>
  </tr>
</template>

<script>
export default {
  props: ["totalCredits2", "value", "id"],
  data() {
    return {
      pointTaken: null,
    };
  },
  watch: {
    pointTaken(point) {
      if (this.pointTaken > 2)
        this.$emit("update:totalCredits2", {
          ...this.totalCredits2,
          [this.id]: point * this.value.credit,
        });
    },
  },
};
</script>

<style></style>
