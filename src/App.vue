<template>
  <div class="bg-gray-200">
    <div class="flex flex-col justify-center h-screen md:items-center">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="w-1/3 mx-auto mt-2 lg:mb-6 lg:w-1/4">
          <img class="" src="./assets/logo.webp" alt="" />
        </div>
        <div
          class="inline-block px-2 py-2 mx-auto align-middle min-w-1/3 lg:px-8"
        >
          <div class="flex items-center mb-1 space-x-2">
            <!-- <div>
              <label
                for="semester"
                class="block text-sm font-medium text-gray-700"
                >Semestrni tanlang</label
              >
              <select
                v-model="selectedSemester"
                @change="semesterChanged($event)"
                id="semester"
                name="semester"
                class="block w-32 py-2 pl-3 pr-10 my-1 text-base border border-gray-300 rounded-md focus:outline-none focus:ring-indigo-500 focus:border-blue-800 sm:text-sm"
              >
                <option
                  v-for="(semester, $semesterIndex) in semesterList"
                  :key="semester"
                  :value="$semesterIndex"
                >
                  {{ semester }}
                </option>
              </select>
            </div> -->
            <div class="w-56 md:flex-1">
              <label for="group" class="block text-sm font-medium text-gray-700"
                >1-Semestr guruhingizni tanlang</label
              >
              <select
                v-model="selectedGroup1"
                id="group"
                name="group"
                class="block w-full py-2 pl-3 pr-10 my-1 text-base border border-gray-300 rounded-md focus:outline-none focus:ring-indigo-500 focus:border-blue-800 sm:text-sm"
              >
                <option
                  v-for="(group, $groupIndex) in groupList1"
                  :key="group.name"
                  :value="$groupIndex"
                >
                  {{ group.name }}
                </option>
              </select>
            </div>
          </div>
          <div v-if="selectedGroup1 !== null" class="flex flex-col">
            <div class="-my-2 sm:-mx-6 lg:-mx-8">
              <div
                class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8"
              >
                <div
                  class="overflow-hidden border-b border-gray-200 sm:rounded-lg"
                >
                  <table class="min-w-full divide-y divide-gray-200">
                    <thead class="bg-gray-100">
                      <tr>
                        <th scope="col" class="text-blue-800 theader">#</th>
                        <th scope="col" class="text-blue-800 theader">
                          Fanlar nomi
                        </th>
                        <th scope="col" class="text-blue-800 theader">
                          Kredit miqdori
                        </th>
                        <th scope="col" class="text-blue-800 theader">
                          Fandan olingan baho
                        </th>
                      </tr>
                    </thead>
                    <tbody>
                      <TableRaw
                        v-for="(group, $subjIndex) in groupList1[selectedGroup1]
                          .subjects"
                        :key="group.name"
                        class="bg-white"
                        :value="group"
                        :id="$subjIndex"
                        :totalCredits.sync="totalCredits"
                      />
                    </tbody>
                    <div class="w-56 md:flex-1 mt-2">
                      <label
                        for="group"
                        class="block text-sm font-medium text-gray-700"
                        >2-Semestr guruhingizni tanlang</label
                      >
                      <select
                        v-model="selectedGroup2"
                        id="group"
                        name="group"
                        class="block w-full py-2 pl-3 pr-10 my-1 text-base border border-gray-300 rounded-md focus:outline-none focus:ring-indigo-500 focus:border-blue-800 sm:text-sm"
                      >
                        <option
                          v-for="(group, $groupIndex) in groupList2"
                          :key="group.name"
                          :value="$groupIndex"
                        >
                          {{ group.name }}
                        </option>
                      </select>
                    </div>
                    <tbody>
                      <TableRaw2
                        v-for="(group, $subjIndex) in groupList2[selectedGroup2]
                          .subjects"
                        :key="group.name"
                        class="bg-white"
                        :value="group"
                        :id="$subjIndex"
                        :totalCredits2.sync="totalCredits2"
                      />
                    </tbody>
                  </table>
                  <div
                    :class="{
                      'bg-green-600': gpa >= 2.7,
                      'bg-red-500': gpa < 2.7,
                      'bg-blue-800': gpa == 0,
                    }"
                    class="flex items-center justify-end py-2"
                  >
                    <div class="mr-4 text-white tdata">
                      Sizning GPA:
                      <span class="ml-2 text-xl font-bold">{{ gpa }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import Table from "./components/Table.vue";
import dataList from "./assets/data/groupList.json";
import TableRaw from "./components/TableRaw.vue";
import TableRaw2 from "./components/TableRaw2.vue";
export default {
  name: "App",
  components: { TableRaw, TableRaw2 },
  data() {
    return {
      totalCredits: {},
      totalCredits2: {},
      selectedGroup1: 0,
      selectedGroup2: 0,
      selectedSemester: 0,
      pointTaken: 0,
      semesterList: [1, 2],
      groupList1: dataList[0],
      groupList2: dataList[1],
    };
  },
  // watch: {
  //   semesterListChange() {
  //     if (this.selectedSemester == 0) {
  //       this.groupList = dataList[0];
  //     } else if (this.selectedSemester == 1) {
  //       this.groupList = dataList[1];
  //       console.log(this.selectedSemester);
  //     }
  //   },
  // },
  // methods: {
  //   semesterChanged(event) {
  //     if (event.target.value == 0) {
  //       this.groupList = dataList[0];
  //     } else if (event.target.value == 1) {
  //       this.groupList = dataList[1];
  //       console.log(event.target.value + "asda");
  //     }
  //   },
  // },
  computed: {
    credit1() {
      return Object.values(this.totalCredits).reduce(
        (prev, curr) => prev + curr,
        0
      );
    },
    credit2() {
      return Object.values(this.totalCredits2).reduce(
        (prev, curr) => prev + curr,
        0
      );
    },
    gpa() {
      return ((this.credit1 + this.credit2) / 60).toFixed(2);
    },
  },
};
</script>

<style>
.theader {
  @apply px-4;
  @apply py-3;
  @apply text-xs;
  @apply font-medium;
  @apply tracking-wider;
  @apply text-left;
  @apply text-gray-500;
  @apply uppercase;
}

.tdata {
  @apply pl-4;
  @apply py-4;
  @apply font-medium;
  @apply text-gray-800;
  @apply whitespace-nowrap;
}
</style>
