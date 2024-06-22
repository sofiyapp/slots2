<template>
    <section>
      <slot name="title">Users</slot>
      <slot
        name="userlist"
        :count="data.results.length"
        :list="data.results"
        :remove="remove"
        v-if="state === 'loaded'"
      >
        <ul class="userlist">
          <li v-for="item in data.results" :key="item.email">
            <slot name="listitem" :user="item">
              <div>
                <img
                  width="48"
                  height="48"
                  :src="item.picture.large"
                  :alt="`${item.name.first} ${item.name.last}`"
                />
                <div>
                  <div>{{ item.name.first }}</div>
                  <slot name="secondrow" :item="item"></slot>
                </div>
              </div>
            </slot>
          </li>
        </ul>
      </slot>
      <slot v-else name="loading">loading...</slot>
      <slot v-if="state === 'failed'" name="error">Oops, something went wrong.</slot>
    </section>
  </template>
  
  <script>
  const states = {
    idle: "idle",
    loading: "loading",
    loaded: "loaded",
    failed: "failed"
  };
  
  export default {
    props: {
      secondrow: {
        type: Function,
        default: () => {}
      }
    },
    data() {
      return {
        state: "idle",
        data: undefined,
        error: undefined,
        states
      };
    },
    mounted() {
      this.load();
    },
    methods: {
      async load() {
        this.state = "loading";
        this.error = undefined;
        this.data = undefined;
        try {
          const response = await fetch("https://randomuser.me/api/?results=5");
          const json = await response.json();
          this.state = "loaded";
          this.data = json;
          return response;
        } catch (error) {
          this.state = "failed";
          this.error = error;
          return error;
        }
      },
      remove(item) {
        this.data.results = this.data.results.filter(entry => entry.email !== item.email);
      }
    }
  };
  </script>
  