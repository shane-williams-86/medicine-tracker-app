<template>
  <div class="home">
    <section class="py-8 py-md-10">
      <div class="container">
        <div class="text-center border-bottom pb-6 mb-7">
          <h1>{{ message }}</h1>
          <p class="text-capitalize line-height-24 h4 mb-5">
            Medicine Tracker makes life easier for caretakers while keeping
            patients and their medicine organized in one space.
          </p>
          <img
            src="https://images.unsplash.com/photo-1587854692152-cbe660dbde88?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8N3x8bWVkaWNhdGlvbnxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=800&q=60"
            alt=""
          />
        </div>
      </div>
    </section>
  </div>
</template>

<style></style>

<script>
export default {
  data: function () {
    return {
      message: "Medicine Tracker",
    };
  },
  created: function () {},
  methods: {},
};
</script>
