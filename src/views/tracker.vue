<!-- eslint-disable -->
<template>
  <div
    class="w-full h-full text-sm sm:text-lg inset-0 fixed bg-white overflow-auto p-2 sm:p-6"
  >
    <div class="h-[90%] cursor-pointer p-6">
      <p class="sm:text-2xl text-lg font-bold pb-8">Validation Tracker</p>

      <p v-if="isRejected" class="text-sm sm:text-lg text-red-500 pb-4">
        Incorrect/Incomplete information has been rejected, click
        <button
          @click="showErrorMessage"
          class="bg-gray-300 px-1 border rounded text-black"
        >
          Here
        </button>
        for more info...
      </p>
      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                class="w-6 h-6 sm:w-8 sm:h-8 relative rounded-full"
                :style="{ 'background-color': checkStage(stage, 1) }"
              >
                <div>
                  <div
                    v-if="stage >= 1 && (reject !== 1 || reject == NaN)"
                    class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                  ></div>
                  <div
                    v-if="stage >= 1 && reject == 1"
                    class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                  ></div>
                  <div
                    v-if="notYetVerified(stage, 1)"
                    class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                  ></div>
                </div>
              </div>
            </div>
          </div>
          <!--text-->
          <div class="relative">
            <button
              @click="showErrorMessage"
              class="p-1 rounded-md text-center capitalize text-white"
              :style="{ 'background-color': checkStage(stage, 1) }"
              :disabled="stage >= 1 && (reject !== 1 || reject == NaN)"
            >
              Number Allocation
            </button>
            <span
              v-if="stage >= 1 && (reject !== 1 || reject == NaN)"
              class="absolute left-0 -bottom-6"
              >{{ numberAllocated }}</span
            >
          </div>
        </div>
        <!--vertical line-->
        <div class="ml-2 sm:ml-3">
          <div
            class="border-l-8 border-l-[#ccc] h-16"
            :style="{ 'border-color': checkStage(stage, 1) }"
          ></div>
        </div>
      </div>

      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                class="w-6 h-6 sm:w-8 sm:h-8 relative rounded-full"
                :style="{ 'background-color': checkStage(stage, 2) }"
              >
                <div
                  v-if="stage >= 2 && (reject !== 2 || reject == NaN)"
                  class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                ></div>
                <div
                  v-if="stage >= 2 && reject == 2"
                  class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                ></div>
                <div
                  v-if="notYetVerified(stage, 2)"
                  class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                ></div>
              </div>
            </div>
          </div>

          <!--text-->
          <button
            @click="showErrorMessage"
            class="p-1 rounded-md text-center capitalize text-white"
            :style="{ 'background-color': checkStage(stage, 2) }"
            :disabled="stage >= 2 && (reject !== 2 || reject == NaN)"
          >
            Area Land Officer
          </button>
        </div>
        <!--vertical line-->
        <div class="ml-2 sm:ml-3">
          <div
            class="border-l-8 border-l-[#ccc] h-16"
            :style="{ 'border-color': checkStage(stage, 2) }"
          ></div>
        </div>
      </div>

      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                class="w-6 h-6 sm:w-8 sm:h-8 relative rounded-full"
                :style="{ 'background-color': checkStage(stage, 3) }"
              >
                <div>
                  <div
                    v-if="stage >= 3 && (reject !== 3 || reject == NaN)"
                    class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                  ></div>
                  <div
                    v-if="stage >= 3 && reject == 3"
                    class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                  ></div>
                  <div
                    v-if="notYetVerified(stage, 3)"
                    class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                  ></div>
                </div>
              </div>
            </div>
          </div>
          <!--text-->
          <button
            @click="showErrorMessage"
            class="p-1 rounded-md text-center capitalize text-white"
            :style="{ 'background-color': checkStage(stage, 3) }"
            :disabled="stage >= 3 && (reject !== 3 || reject == NaN)"
          >
            Director Land 1
          </button>
        </div>
        <!--vertical line-->
        <div class="ml-2 sm:ml-3">
          <div
            class="border-l-8 border-l-[#ccc] h-16"
            :style="{ 'border-color': checkStage(stage, 3) }"
          ></div>
        </div>
      </div>

      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                class="w-6 h-6 sm:w-8 sm:h-8 relative bg-[#ccc] rounded-full"
                :style="{ 'background-color': checkStage(stage, 4) }"
              >
                <div
                  v-if="stage >= 4 && (reject !== 4 || reject == NaN)"
                  class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                ></div>
                <div
                  v-if="stage >= 4 && reject == 4"
                  class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                ></div>
                <div
                  v-if="notYetVerified(stage, 4)"
                  class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                ></div>
              </div>
            </div>
          </div>
          <!--text-->
          <button
            @click="showErrorMessage"
            :style="{ 'background-color': checkStage(stage, 4) }"
            :disabled="stage >= 4 && (reject !== 4 || reject == NaN)"
            class="p-1 rounded-md text-center capitalize text-white bg-[#ccc]"
          >
            Surveyor General
          </button>
        </div>
        <!--vertical line-->
        <div class="ml-2 sm:ml-3">
          <div
            class="border-l-8 border-l-[#ccc] h-16"
            :style="{ 'border-color': checkStage(stage, 4) }"
          ></div>
        </div>
      </div>

      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                :style="{ 'background-color': checkStage(stage, 5) }"
                class="w-6 h-6 sm:w-8 sm:h-8 relative bg-[#ccc] rounded-full"
              >
                <div
                  v-if="stage >= 5 && (reject !== 5 || reject == NaN)"
                  class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                ></div>
                <div
                  v-if="stage >= 5 && reject == 5"
                  class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                ></div>
                <div
                  v-if="notYetVerified(stage, 5)"
                  class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                ></div>
              </div>
            </div>
          </div>
          <!--text-->
          <button
            @click="showErrorMessage"
            :style="{ 'background-color': checkStage(stage, 5) }"
            :disabled="stage >= 5 && (reject !== 5 || reject == NaN)"
            class="p-1 rounded-md text-center capitalize text-white bg-[#ccc]"
          >
            Cartography
          </button>
        </div>
        <!--vertical line-->
        <div class="ml-2 sm:ml-3">
          <div
            class="border-l-8 border-l-[#ccc] h-16"
            :style="{ 'border-color': checkStage(stage, 5) }"
          ></div>
        </div>
      </div>

      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                :style="{ 'background-color': checkStage(stage, 6) }"
                class="w-6 h-6 sm:w-8 sm:h-8 relative bg-[#ccc] rounded-full"
              >
                <div
                  v-if="stage >= 6 && (reject !== 6 || reject == NaN)"
                  class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                ></div>
                <div
                  v-if="stage >= 6 && reject == 6"
                  class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                ></div>
                <div
                  v-if="notYetVerified(stage, 6)"
                  class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                ></div>
              </div>
            </div>
          </div>
          <!--text-->
          <button
            @click="showErrorMessage"
            :style="{ 'background-color': checkStage(stage, 6) }"
            :disabled="stage >= 6 && (reject !== 6 || reject == NaN)"
            class="p-1 rounded-md text-center capitalize text-white bg-[#ccc]"
          >
            Town Planner
          </button>
        </div>
        <!--vertical line-->
        <div class="ml-2 sm:ml-3">
          <div
            class="border-l-8 border-l-[#ccc] h-16"
            :style="{ 'border-color': checkStage(stage, 6) }"
          ></div>
        </div>
      </div>

      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                :style="{ 'background-color': checkStage(stage, 7) }"
                class="w-6 h-6 sm:w-8 sm:h-8 relative bg-[#ccc] rounded-full"
              >
                <div
                  v-if="stage >= 7 && (reject !== 7 || reject == NaN)"
                  class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                ></div>
                <div
                  v-if="stage >= 7 && reject == 7"
                  class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                ></div>
                <div
                  v-if="notYetVerified(stage, 7)"
                  class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                ></div>
              </div>
            </div>
          </div>
          <!--text-->
          <button
            @click="showErrorMessage"
            :style="{ 'background-color': checkStage(stage, 7) }"
            :disabled="stage >= 7 && (reject !== 7 || reject == NaN)"
            class="p-1 rounded-md text-center capitalize text-white bg-[#ccc]"
          >
            Director Land 2
          </button>
        </div>
        <!--vertical line-->
        <div class="ml-2 sm:ml-3">
          <div
            class="border-l-8 border-l-[#ccc] h-16"
            :style="{ 'border-color': checkStage(stage, 7) }"
          ></div>
        </div>
      </div>

      <div class="flex flex-col">
        <div class="flex items-center">
          <div class="sm:w-24 w-16 bg-none">
            <div>
              <!--large circle-->
              <div
                :style="{ 'background-color': checkStage(stage, 8) }"
                class="w-6 h-6 sm:w-8 sm:h-8 relative bg-[#ccc] rounded-full"
              >
                <div
                  v-if="stage >= 8 && (reject !== 8 || reject == NaN)"
                  class="sm:w-2 w-[5px] h-[9px] mx-[9px] my-[6px] sm:border-b-4 border-b-2 border-r-2 sm:border-r-4 transform rotate-45 sm:h-4 absolute inset-0 border-white sm:m-auto"
                ></div>
                <div
                  v-if="stage >= 8 && reject == 8"
                  class="w-2 h-2 absolute inset-0 bg-white m-auto rounded-full"
                ></div>
                <div
                  v-if="notYetVerified(stage, 8)"
                  class="w-4 h-1 absolute inset-0 bg-white m-auto rounded-lg"
                ></div>
              </div>
            </div>
          </div>
          <!--text-->
          <button
            @click="showErrorMessage"
            :style="{ 'background-color': checkStage(stage, 8) }"
            :disabled="stage >= 8 && (reject !== 8 || reject == NaN)"
            class="p-1 rounded-md text-center capitalize text-white bg-[#ccc]"
          >
            N.I.G.I.S
          </button>
        </div>
        <!--vertical line-->
      </div>

      <!---->
      <div class="none py-10">
        <!-- Certificates -->
        <div v-if="stage === 8">
          <div class="text-center font-bold text-black text-2xl mt-5">
            Congratulations!!!
          </div>
          <p class="text-center mb-1">
            Your C of O Certificate is Finally Ready
          </p>
          <div class="w-11/12 mx-auto h-full ">
            <img class="w-full h-full" src="/cofo.jpeg" />
          </div>
          <div class="flex justify-center">
            <a
              download="C of O"
              href="/cofo.jpeg"
              class="mt-4 text-blue-500 text-2xl font-bold"
              >Download</a
            >
          </div>
        </div>
      </div>
    </div>
    <div class="fixed -z-40 m-auto inset-0 w-1/2 h-4/5">
      <img
        class="w-full h-full opacity-10"
        src="../assets/images/nigislogo.png"
      />
    </div>

    <!---Rejection message-->
    <div
      @click.self="showErrorMessage"
      :class="noMessage ? 'hidden' : 'block'"
      class="fixed h-full w-full inset-0 bg-black bg-opacity-50"
    >
      <div
        class="absolute space-y-6 m-auto inset-0 w-3/5 sm:w-[300px] h-fit p-8 bg-white rounded-lg text-center"
      >
        <p>{{ message }}</p>

        <button
          @click="gotoForm"
          class="rounded-md py-1 px-2 bg-[#0c8824] text-white"
        >
          Fill the form
        </button>
      </div>
    </div>
  </div>
</template>
<!--eslint-disable-->
<script>
/* eslint-disable */
import axios from "@/utils/useAxios";
import { mapGetters } from "vuex";

export default {
  name: "TrackerPage",
  components: {},

  data() {
    return {
      numberAllocated: "",
      stage: "",
      reject: NaN,
      notChecked: true,
      message: "",
      noMessage: true,
      isRejected: false,
      data: null,
    };
  },
  computed: {
    ...mapGetters(["getCurrentUser"]),
  },
  mounted() {
    this.getUserStage();
  },

  methods: {
    getUserStage() {
      axios
        .get(`requirement/tracker/${this.getCurrentUser._id}`)
        .then((response) => {
          const { data } = response.data;
          this.data = data;
          console.log(data);
          this.numberAllocated = data.numberAllocated;
          this.stage = data.stage;
          this.reject = parseInt(data.reject);
          this.message = data.message;
          if (this.message !== "") {
            this.isRejected = !this.isRejected;
          }
        });
    },
    checkStage(stage, currentStage) {
      if (stage >= currentStage && this.reject == currentStage) {
        return "#CC0000";
      } else if (stage >= currentStage) {
        return "#0c8824";
      } else {
        return "#E0E0E0";
      }
    },
    notYetVerified(stage, currentStage) {
      if (stage < currentStage) {
        return this.notChecked;
      }
    },
    showErrorMessage() {
      this.noMessage = !this.noMessage;
      //console.log("clicked");
    },
    gotoForm() {
      this.$router.push("/form");
    },
  },
};
</script>

<style scoped>
/* eslint-disable */

html,
body {
  left: 0;
  top: 0;
  height: 100%;
  width: 100%;
}
</style>
<!--eslint-disable-->
