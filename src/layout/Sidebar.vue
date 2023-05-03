<template>
  <div
    class="sidebar p-5 bg-dark text-white"
    :class="IS_COLLAPSED ? 'w-[250px]' : 'w-auto'"
  >
    <div class="logo flex justify-space-between relative">
      <img
        src="../assets/logo.png"
        alt="logo"
        class="rounded-full"
        :class="IS_COLLAPSED ? 'w-12' : 'w-10'"
      />
      <transition>
        <span
          v-if="IS_COLLAPSED"
          class="absolute ml-2 text-2xl uppercase font-semibold ml-15"
          >Google
        </span>
      </transition>
    </div>

    <ul class="py-5 mt-5 relative">
      <li
        :class="{ 'bg-brand': item.childs.includes($route.name) }"
        v-for="item in menuItems"
        :key="item.name"
        @click="$router.push({ name: item.routeName })"
        class="cursor-pointer text-xl mb-2 p-2 rounded-md"
      >
        <i :class="item.icon"></i>
        <transition>
          <span class="ml-3 absolute" v-if="IS_COLLAPSED">{{ item.name }}</span>
        </transition>
      </li>
    </ul>
  </div>
</template>

<script>
import menuItems from "./menuConfig";
import { mapGetters } from "vuex";
export default {
  data() {
    return {
      menuItems,
    };
  },
  computed: {
    ...mapGetters("ui", ["IS_COLLAPSED"]),
  },
};
</script>

<style scoped>
.sidebar {
  /* width: 250px; */
  height: 100vh;
}
.logo {
  display: flex;
  align-items: center;
  justify-content: center;
}
img {
  width: 50px;
  margin-right: 10px;
}
.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease;
  width: 0px;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
  width: auto;
}
</style>
