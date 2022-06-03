<template>
  <div class="app">
    <header>
      <div class="title">
        <a-typography-title>Job List</a-typography-title>
      </div>
      <div class="order">
        <a-button @click="handleClick('title')" type="block">
          order by title</a-button
        >
        <a-divider type="vertical" />
        <a-button @click="handleClick('salary')" type="block"
          >order by salary</a-button
        >
        <a-divider type="vertical" />
        <a-button @click="handleClick('location')" type="block"
          >order by location</a-button
        >

        <!-- <button @click="handleClick('title')">order by title</button> -->
        <!-- <button @click="handleClick('salary')">order by salary</button> -->
        <!-- <button @click="handleClick('location')">order by location</button> -->
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import JobList from "./components/JobList.vue";
import Job from "./types/index";
import OrderTerm from "./types/OrderTerm";

export default defineComponent({
  name: "App",
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      {
        id: "1",
        title: "Frontend",
        location: "Google",
        salary: 1000,
      },
      {
        id: "2",
        title: "Backend",
        location: "Facebook",
        salary: 2000,
      },
      {
        id: "3",
        title: "Fullstack",
        location: "Apple",
        salary: 3000,
      },
      {
        id: "4",
        title: "Devops",
        location: "Amazon",
        salary: 4000,
      },
      {
        id: "5",
        title: "QA",
        location: "Microsoft",
        salary: 5000,
      },
    ]);

    const order = ref<OrderTerm>("title");
    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };

    return { jobs, handleClick, order };
  },
});
</script>

<style>
header {
  text-align: center;
}
header .order {
  margin-top: 20px;
}
.order {
  margin: 20px auto;
}

a-button {
  margin-right: 20px;
}
header .title {
  display: flex;
  justify-content: center;
}
header img {
  width: 60px;
  margin-right: 20px;
}
.title {
  margin-top: 30px;
}
</style>
