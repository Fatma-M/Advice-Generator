<template>
  <main>
    <section>
      <div class="advice-number">
        <p>
          advice <span>#{{ adviceId }}</span>
        </p>
      </div>
      <div class="advice-content">
        <p>
          {{ adviceText }}
        </p>
        <img
          src="./assets/Spinner.svg"
          alt="spinner"
          class="spinner-icon"
          v-show="isLoading"
        />
      </div>
      <div class="advice-icon">
        <img src="./assets/pattern-divider-desktop.svg" alt="" />
      </div>
      <div class="advice-btn">
        <button @click="getAdvice">
          <img src="./assets/icon-dice.svg" alt="" />
        </button>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      adviceText: "",
      adviceId: null,
      isLoading: false,
    };
  },

  mounted() {
    this.getAdvice();
  },

  methods: {
    getAdvice() {
      this.isLoading = true;
      fetch("https://api.adviceslip.com/advice")
        .then((response) => {
          if (response.ok) {
            return response.json();
          }
        })
        .then((data) => {
          if (data) {
            let adviceObj = data.slip;
            setTimeout(() => {
              this.adviceText = adviceObj.advice;
              this.adviceId = adviceObj.id;
              this.isLoading = false;
            }, 500);
          }
        });
    },
  },
};
</script>
