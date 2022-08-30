<script>
import moment from "moment";
import Register from "./Register/index.vue";
import Candidates from "./Candidates/index.vue";
export default {
  components: { Register },
  data() {
    return {
      state: {
        id: 0,
        title: "before vote",
      },
      countdown: {},
      candidates: [
        {
          photo: "https://cdn-icons-png.flaticon.com/512/146/146031.png",
          name: "آقای محمد علی عزیزی",
        },
        {
          photo: "https://cdn-icons-png.flaticon.com/512/146/146031.png",
          name: "آقای محمد علی عزیزی",
        },
        {
          photo: "https://cdn-icons-png.flaticon.com/512/146/146031.png",
          name: "آقای محمد علی عزیزی",
        },
        {
          photo: "https://cdn-icons-png.flaticon.com/512/146/146031.png",
          name: "آقای محمد علی عزیزی",
        },
      ],
    };
  },
  mounted() {
    setTimeout(() => {
      this.state.id = 1;
      this.startTimer();
    }, 3000);
  },
  methods: {
    startTimer() {
      const endTime = moment("2022-08-18 22:30:00");
      const eventTime = moment("2022-08-18 20:20:00");
      const currentTime = moment();
      var duration = moment.duration(eventTime.diff(currentTime));
      const interval = 1000;
      let voteInterval = setInterval(() => {
        duration = moment.duration(duration - interval, "milliseconds");
        this.countdown["days"] = duration.days();
        this.countdown["hours"] = duration.hours();
        this.countdown["minutes"] = duration.minutes();
        this.countdown["seconds"] = duration.seconds();

        if (moment.duration(endTime.diff(currentTime)).seconds() < 0) {
          this.state.id = 3;
          clearInterval(voteInterval);
        } else if (this.countdown.seconds < 0) {
          this.state.id = 2;
          clearInterval(voteInterval);
        }
      }, interval);
    },
  },
  components: { Register, Candidates },
};
</script>

<template>
  <div class="vote">
    <h1 v-if="state.id === 0" class="vote-welcome">
      به سامانه انتخابات خوش آمدید
    </h1>

    <div v-else-if="state.id === 1" class="vote-remaning">
      <h2>زمان باقی مانده تا انتخابات:</h2>
      <div class="vote-remaning__warpper">
        <span class="vote-remaning__countdown">
          <div>{{ countdown.days }}</div>
          <div>روز</div>
        </span>
        <span class="vote-remaning__countdown">
          <div>{{ countdown.hours }}</div>
          <div>ساعت</div>
        </span>
        <span class="vote-remaning__countdown">
          <div>{{ countdown.minutes }}</div>
          <div>دقیقه</div>
        </span>
        <span class="vote-remaning__countdown">
          <div>{{ countdown.seconds }}</div>
          <div>ثانیه</div>
        </span>
      </div>

      <div class="vote-candidates">
        <div
          class="vote-candidates__person"
          v-for="(candidate, index) in candidates"
          :key="index"
        >
          <img :src="candidate.photo" :alt="candidate.name" />
          <span>{{ candidate.name }}</span>
        </div>
      </div>
    </div>

    <Register v-else-if="state.id === 2" />
    <Candidates v-else-if="state.id === 3" />
  </div>
</template>

<style scoped lang="scss" src="./MainComponent.scss" />
