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
        </div>

        <div class="row">
          <div class="col-md-6 col-lg-4">
            <div class="media mb-4 mb-md-6 mb-lg-7">
              <a
                href="javascript:void(0)"
                class="
                  icon-item-default
                  border
                  rounded
                  border-dark
                  bg-dark
                  text-white
                  me-5
                "
              >
                <i class="fa fa-bell" aria-hidden="true"></i>
              </a>

              <div class="media-body">
                <h4 class="text-capitalize font-weight-bold">
                  Donec vel libero
                </h4>
                <p>
                  Donec vel libero non lorem pharetra efficitur. Nunc nibh elit,
                  consectetur quis dapibu.
                </p>
              </div>
            </div>
          </div>

          <div class="col-md-6 col-lg-4">
            <div class="media mb-4 mb-md-6 mb-lg-7">
              <a
                href="javascript:void(0)"
                class="
                  icon-item-default
                  border
                  rounded
                  border-dark
                  bg-dark
                  text-white
                  me-5
                "
              >
                <i class="fa fa-briefcase" aria-hidden="true"></i>
              </a>

              <div class="media-body">
                <h4 class="text-capitalize font-weight-bold">
                  Vivamus laoreet
                </h4>
                <p>
                  Vivamus laoreet dui quis interdum volutpat. Integer in magna
                  sit amet efficitur nec.
                </p>
              </div>
            </div>
          </div>

          <div class="col-md-6 col-lg-4">
            <div class="media mb-4 mb-md-6 mb-lg-7">
              <a
                href="javascript:void(0)"
                class="
                  icon-item-default
                  border
                  rounded
                  border-dark
                  bg-dark
                  text-white
                  me-5
                "
              >
                <i class="fas fa-taxi" aria-hidden="true"></i>
              </a>

              <div class="media-body">
                <h4 class="text-capitalize font-weight-bold">
                  Ullamcorper congue
                </h4>
                <p>
                  Ullamcorper congue lorem ac pharetra laoreet. Nam magna mi,
                  eleifend ac vulpu.
                </p>
              </div>
            </div>
          </div>

          <div class="col-md-6 col-lg-4">
            <div class="media mb-4 mb-md-6 mb-lg-0">
              <a
                href="javascript:void(0)"
                class="
                  icon-item-default
                  border
                  rounded
                  border-dark
                  bg-dark
                  text-white
                  me-5
                "
              >
                <i class="fa fa-camera" aria-hidden="true"></i>
              </a>

              <div class="media-body">
                <h4 class="text-capitalize font-weight-bold">
                  Proin libero erat
                </h4>
                <p>
                  Proin libero erat lectus auctor viverra. Praesent sollicitudin
                  leo velit sed, semper diam.
                </p>
              </div>
            </div>
          </div>

          <div class="col-md-6 col-lg-4">
            <div class="media mb-4 mb-md-0">
              <a
                href="javascript:void(0)"
                class="
                  icon-item-default
                  border
                  rounded
                  border-dark
                  bg-dark
                  text-white
                  me-5
                "
              >
                <i class="fa fa-cloud" aria-hidden="true"></i>
              </a>

              <div class="media-body">
                <h4 class="text-capitalize font-weight-bold">Amaiging tour</h4>
                <p>
                  Amaiging tour leo vitae convallis sollicitudin. Nulla volutpat
                  dapibus at pellen.
                </p>
              </div>
            </div>
          </div>

          <div class="col-md-6 col-lg-4">
            <div class="media">
              <a
                href="javascript:void(0)"
                class="
                  icon-item-default
                  border
                  rounded
                  border-dark
                  bg-dark
                  text-white
                  me-5
                "
              >
                <i class="fas fa-utensils" aria-hidden="true"></i>
              </a>

              <div class="media-body">
                <h5 class="text-capitalize font-weight-bold">
                  Cras vestibulum
                </h5>
                <p>
                  Cras vestibulum, nisl et volutpat dapibus, nisl odio accumsan
                  pretium lacus.
                </p>
              </div>
            </div>
          </div>
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
      message: "Welcome to Medicine Tracker",
    };
  },
  created: function () {},
  methods: {},
};
</script>
