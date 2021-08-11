<template>
  <div class="container">
    <section class="section py-5">
      <div class="row">
        <div class="col-md-10 m-auto">
          <input
            type="search"
            name="search"
            id="search"
            class="form-control"
            placeholder="Search by username or name"
            v-model="search"
            @keypress="getDetails"
          />
        </div>
        <div class="col-md-2 m-auto">
          <button type="button" class="btn btn-primary m-1" @click="getDetails">
            Search!
          </button>
          <button type="button" class="btn btn-danger m-1" @click="getCleared">
            Clear
          </button>
        </div>
      </div>
    </section>
    <section class="section py-5">
      <div class="row">
        <div class="col-md-10-m-auto">
          <div class="row" v-if="githubUsers.length != 0">
            <div
              class="col-md-4"
              v-for="(user, index) in githubUsers"
              :key="index"
            >
              <a :href="user.html_url" target="_blank">
                <div class="card text-center">
                  <div class="card-body">
                    <img
                      :src="user.avatar_url"
                      alt=""
                      width="150px"
                      height="150px"
                    />
                    <h4 class="card-title py-2">
                      {{ user.login }}
                    </h4>
                  </div>
                </div>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "Body",
  data() {
    return {
      githubUsers: [],
      search: "",
    };
  },
  methods: {
    async getDetails() {
      const searchText = this.search.trim();
      let res = await axios.get(
        `https://api.github.com/search/users?q=${searchText}&client_id=9a632cb16e2e3def018a&client_secret=12e9c732822166db4732e062a8cd67504767ee46`
      );
      // let data = res.json();
      console.log(res.data.items);
      if (res.data.items != null) {
        this.githubUsers = res.data.items;
      } else {
        this.githubUsers = [];
      }
    },
    getCleared() {
      this.githubUsers = [];
      this.search = "";
    },
  },
};
</script>

<style scoped>
  img {
    border-radius: 50%;
  }

  a {
    text-decoration: none;
  }

  .card-title {
    color: #363636;
  }
</style>