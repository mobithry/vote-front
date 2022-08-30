<script>
export default {
  name: "Candidates",
  data() {
    return {
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
};
</script>

<template>
  <div class="candidates">
    <h2 align="center">نتایج انتخابات</h2>
    <div
      class="candidates-card"
      v-for="candidate in candidates"
      :key="candidate.id"
    >
      <img :src="photo" :alt="candidate.name" />
      <span>
        {{ candidate.name }} <br />
        تعداد آرا : {{ candidate.count }}</span
      >
    </div>
  </div>
</template>

<style src="./style.scss" />
