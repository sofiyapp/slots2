<template>
  <div class="page">
    <select v-model="selected">
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
      >{{ option.label }}</option>
    </select>

    <AppUserList>
      <template v-slot:title>
        <h2>Users List</h2>
      </template>
      <template v-slot:userlist="{ list }">
        <AppUserCardList :list="list">
          <template v-slot:first="{ text }">
            <h4>{{ text }}</h4>
          </template>
        </AppUserCardList>
      </template>
      <template v-slot:loading>
        <p>Loading users...</p>
      </template>
      <template v-slot:error>
        <p>Oops, something went wrong!</p>
      </template>
    </AppUserList>
  </div>
</template>

<script>
import AppUserCardList from "@/components/AppUserCardList.vue";
import AppUserList from "@/components/AppUserList.vue";

export default {
  components: {
    AppUserList,
    AppUserCardList
  },
  data() {
    return {
      selected: "first",
      options: [
        { value: "first", label: "First Name" },
        { value: "last", label: "Last Name" },
        { value: "full", label: "Full Name" },
        { value: "fullWithTitle", label: "Full Name with Title" }
      ]
    };
  }
};
</script>

<style>
.page {
  padding: 2rem;
}
.page > * + * {
  margin-top: 2rem;
}
</style>
