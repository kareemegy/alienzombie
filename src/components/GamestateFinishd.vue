<template>
  <div class="modal">
    <h1 v-if="uiState == 'won'">You're won.</h1>
    <h1 v-if="uiState == 'lost'">You're lost.</h1>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 131 131"
      aria-labelledby="face"
      role="presentation"
      width="70"
      height="70"
      id="face"
    >
      <title id="face">Face Icon</title>
      <circle class="cls-1" cx="65.5" cy="65.5" r="64" />
      <circle class="cls-2" cx="95" cy="65.8" r="7.5" />
      <circle class="cls-2" cx="36" cy="65.8" r="7.5" />
      <path
        id="mouth"
        class="cls3"
        d="M51,97s6,10,23,10S95,97,95,97"
        transform="translate(-8.5 -5.5)"
      />
    </svg>
    <button @click="restartTheGame">Let's play agein</button>
  </div>
</template>

<script>
import { mapState } from "vuex";
import gsap from "gsap";
export default {
  computed: {
    ...mapState(["uiState", "Score", "questionIndex"]),
  },
  methods: {
    restartTheGame() {
      this.$store.commit("resetGame");
    },
  },
  mounted() {
    if (this.$store.state.uiState == "lost") {
      gsap.to("#face", {
        duration: 1,
        rotation: "360",
        ease: "easeIn",
        repeat: -1,
      });
    }
  },
};
</script>

<style lang="scss" scoped>
.modal {
  display: flex;
  flex-direction: column;
  align-items: center;
  left: calc(50% - 200px) !important;
  top: 145px !important;
}
button {
  margin-top: 30px;
  padding: 16px;
}
.cls-1 {
  fill: #fbb040;
  stroke: #231f20;
}

.cls-1,
.cls-3 {
  stroke-miterlimit: 10;
  stroke-width: 3px;
}

.cls-2 {
  fill: #231f20;
}

.cls-3 {
  fill: none;
  stroke: #be1e2d;
}
</style>
