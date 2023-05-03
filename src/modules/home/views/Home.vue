<template>
  <v-container>
    <v-card class="p-5">
      <div class="head flex justify-between items-center mb-7">
        <h2 class="text-3xl text-gray-600 font-bold">Users</h2>

        <v-btn class="bg-green-600 text-white" @click="createUser = true">
          <i class="fas fa-plus"></i>
          <span class="ml-2">Create New</span>
        </v-btn>
      </div>

      <!--  -->
      <Table :headers="headers" :items="items">
        <!--  -->
        <template #item-avatar="user">
          <div class="flex justify-center">
            <v-avatar class="bg-brand">
              <i v-if="!user.photo" class="fas fa-user text-white"></i>
              <img
                v-else
                :src="mediaUrl + user.photo"
                :alt="user.username"
                class="w-full h-full object-cover"
              />
            </v-avatar>
          </div>
        </template>

        <!--  -->
        <template #item-name="user">
          <div class="text-center font-semibold">
            {{ user.first_name }}
            {{ user.last_name }}
          </div>
        </template>

        <!--  -->
        <template #item-username="user">
          <div class="text-center font-semibold">
            {{ user.username }}
          </div>
        </template>

        <!--  -->
        <template #item-phone_number="user">
          <div class="text-center">
            <a :href="'tel:' + user.phone_number" class="text-brand"
              >{{ user.phone_number }}
            </a>
          </div>
        </template>

        <!--  -->
        <template #item-email="user">
          <div class="text-center">
            <a :href="'mailto: ' + user.email" class="text-brand"
              >{{ user.email }}
            </a>
          </div>
        </template>

        <!--  -->
        <template #item-created_at="user">
          <div class="text-center">
            {{ new Date(user.created_at).toLocaleString() }}
          </div>
        </template>

        <!--  -->
        <template #item-action="user">
          <div class="flex justify-center items-center my-2">
            <v-btn class="bg-blue-600 text-white mr-2" @click="editUser = user">
              <i class="fas fa-edit"></i>
            </v-btn>

            <v-btn
              class="bg-red-600 text-white"
              @click="deleteUserDialog = user._id"
            >
              <i class="fas fa-trash"></i>
            </v-btn>
          </div>
        </template>
      </Table>

      <!--  -->
    </v-card>
  </v-container>
</template>

<script>
import Table from "@/components/TheTable.vue";
import usersArray from "./usersArray";

export default {
  components: { Table },
  data() {
    return {
      headers: [
        { text: "ID", value: "id" },
        { text: "Name", value: "name", sortable: true },
        { text: "Date", value: "date", sortable: true },
        { text: "Price", value: "price", sortable: true },
        { text: "Status", value: "status", sortable: true },
        { text: "Action", value: "action" },
      ],
      items: usersArray,
    };
  },
};
</script>
