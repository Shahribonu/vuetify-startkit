<template>
  <div
    class="profile-menu px-5 py-2 flex items-center justify-between border-b-2 border-gray-300"
  >
    <div class="sidebar-toggler-wrapper h-full">
      <div
        class="sidebar-toggler w-9 h-full shadow-md rounded-md p-1 cursor-pointer flex"
        @click="toggleSidebar"
      >
        <div
          :class="IS_COLLAPSED ? 'ml-auto' : 'mr-auto'"
          class="sidebar-toggler-item w-1/2 h-full bg-brand rounded-md transition-all"
        ></div>
      </div>
    </div>

    <!-- user -->
    <div class="user-info flex items-center">
      <div class="text-content">
        <h4 class="user-name text-xl font-semibold text-gray-800 leading-3">
          {{ userInfo.username }}
        </h4>
        <p class="text-xs font-semibold text-gray-500 text-right">
          {{ userInfo.email }}
        </p>
      </div>
      <div class="profile-pic ml-2">
        <v-avatar color="info">
          <img src="../assets/404.png" alt="image" v-if="profileImage" />
          <i v-else class="fas fa-user"> </i>
        </v-avatar>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import { fetchUserInfo } from "../api/auth";
export default {
  data() {
    return {
      profileImage: "@/assets/404.png",
      isCollapsed: false,
      userInfo: "",
    };
  },
  computed: {
    ...mapGetters("ui", ["IS_COLLAPSED"]),
  },
  methods: {
    ...mapActions("ui", ["TOGGLE_SIDEBAR"]),
    toggleSidebar() {
      this.TOGGLE_SIDEBAR();
    },
  },
  async mounted() {
    const res = await fetchUserInfo();
    this.userInfo = res;
  },
};
</script>

<style></style>
