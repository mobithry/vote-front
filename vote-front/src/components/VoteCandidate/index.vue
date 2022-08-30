<script>
import moment from "moment";
export default {
  name: "VoteCandidate",
  data() {
    return {
      voteSubmitted: false,
      countdown: {},
      candidates: [
        {
          id: 1,
          name: "مهران تهرانی",
          count: 123,
        },
        {
          id: 1,
          name: "مهران تهرانی",
          count: 60,
        },
        {
          id: 1,
          name: "مهران تهرانی",
          count: 50,
        },
        {
          id: 1,
          name: "مهران تهرانی",
          count: 22,
        },
      ],
      photo: "https://cdn-icons-png.flaticon.com/512/146/146031.png",
    };
  },

  mounted() {
    this.startTimer();
  },

  methods: {
    submitVote(candidate) {
      console.log(candidate);
      this.voteSubmitted = true;
    },

    startTimer() {
      const endTime = moment("2022-08-18 17:30:00");
      const eventTime = moment("2022-09-17");
      const currentTime = moment();
      var duration = moment.duration(eventTime.diff(currentTime));
      const interval = 1000;
      const voteInterval = setInterval(() => {
        duration = moment.duration(duration - interval, "milliseconds");
        this.countdown["days"] = duration.days();
        this.countdown["hours"] = duration.hours();
        this.countdown["minutes"] = duration.minutes();
        this.countdown["seconds"] = duration.seconds();

        if (moment.duration(currentTime.diff(endTime)).seconds() < 0) {
          this.state.id = 3;
          clearInterval(voteInterval);
        }
      }, interval);
    },
  },
};
</script>

<template>
  <div class="vote-candidate">
    <template v-if="!voteSubmitted">
      <span class="vote-candidate__info">اطالاعات هویتی شما تایید شد.</span>
      <h2 align="center">کاندید مورد نظر خود را انتخاب نمایید.</h2>
      <div class="vote-candidate-wrapper">
        <div
          @click="submitVote(candidate)"
          class="vote-candidate-card"
          v-for="candidate in candidates"
          :key="candidate.id"
        >
          <img :src="photo" :alt="candidate.name" />
          <span>{{ candidate.name }}</span>
        </div>
      </div>
    </template>
    <div v-else>
      <h2 align="center" class="vote-candidate__message">
        رای شما ثبت شد، تشکر می‌کنیم از اینکه در انتخابات شرکت کردید
      </h2>

      <div class="vote-candidate__warpper">
        <span class="vote-candidate__countdown">
          <div>{{ countdown.days }}</div>
          <div>روز</div>
        </span>
        <span class="vote-candidate__countdown">
          <div>{{ countdown.hours }}</div>
          <div>ساعت</div>
        </span>
        <span class="vote-candidate__countdown">
          <div>{{ countdown.minutes }}</div>
          <div>دقیقه</div>
        </span>
        <span class="vote-candidate__countdown">
          <div>{{ countdown.seconds }}</div>
          <div>ثانیه</div>
        </span>
      </div>
      <h3 align="center" class="vote-candidate__end-vote">تا پایان اتنخابات</h3>
    </div>
  </div>
</template>

<style src="./style.scss" />
