<template>
  <div>
    <FlashMessage :position="'right bottom'"></FlashMessage>
    <div class="container">
      <div class="row">
        <div class="col-md-10 offset-1 ml-3 m-5">
          <img
            :src="'/uploads/' + this.annonce[0].image"
            alt=""
            height="500px"
            width="1000px"
          />
          <p class="text-center">
            <strong>{{ this.annonce[0].titre }}</strong>
          </p>
          <p>
            {{ this.annonce[0].contenu }}
          </p>
          <p>
            <small>{{ this.annonce[0].description }}</small>
          </p>

          <form @submit.prevent="handleSubmit">
            <span style="size: 100px">
              <button class="btn btn-round" style="text-decoration: none">
                <i class="fa fa-check" aria-hidden="true"></i>
                Interesse
              </button>
            </span>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Show",
  props: ["annonce"],
  methods: {
    handleSubmit() {
      const data = new FormData();
      data.append("annonce_id", this.annonce[0].id);
      data.append("annonce_image", this.annonce[0].image);
      data.append("annonce_titre", this.annonce[0].titre);
      data.append("post_id", this.annonce[0].user_id);

      this.$inertia.post("/Annonce/interesse/" + this.annonce[0].id, data, {
        onSuccess: () => {
          window.location("/interesseRedirect");
        },
      });
    },
  },
};
</script>

<style>
</style>
