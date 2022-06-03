<template>
  <div class="job-list">
    <a-typography-title :level="3">Ordered By {{ order }}</a-typography-title>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <a-card hoverable>
          <a-typography-title :level="3"
            >{{ job.title }} in {{ job.location }}</a-typography-title
          >
          <div class="salary">
            <img src="../assets/rupee.svg" alt="rupee icon" />
            <p>{{ job.salary }} pounds</p>
          </div>
          <div class="description">
            <a-typography-text strong>
              Lorem ipsum dolor sit amet consectetur, adipisicing elit. Autem
              quia recusandae perferendis. Ea quos quaerat odio rerum
              perspiciatis minus officiis vero dolorem provident necessitatibus
              asperiores error nesciunt, velit, dignissimos eius?
            </a-typography-text>
          </div>
        </a-card>
      </li>
    </transition-group>
  </div>
</template>
<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "@/types/index";
import OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      type: Array as PropType<Job[]>,
      required: true,
    },
    order: {
      type: String as PropType<OrderTerm>,
      required: true,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] < b[props.order] ? 1 : -1;
      });
    });

    return { orderedJobs };
  },
});
</script>

<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 30px;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
.list-move {
  transition: all 1s;
}
</style>