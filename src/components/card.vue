<template>
  <div class="col-md-3">
    <div class="card mb-4 box-shadow">
      <img
        class="card-img-top"
        data-src="holder.js/100px225?theme=thumb&amp;bg=55595c&amp;fg=eceeef&amp;text=Thumbnail"
        alt="Thumbnail [100%x225]"
        v-bind:src="url"
        data-holder-rendered="true"
      />
      <div class="card-body">
        <p class="card-text">
          <b>{{ title }}</b>
        </p>
        <p class="card-text">{{ body }}</p>
        <div class="d-flex justify-content-between align-items-center">
          <div class="btn-group">
            <button type="button" class="btn btn-sm btn-outline-secondary">
              View
            </button>
            <button type="button" class="btn btn-sm btn-outline-secondary">
              Edit
            </button>
          </div>
          <small class="text-muted">9 mins</small>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    title: String,
    body: String,
    url: {
      type: String,
      default: "https://picsum.photos/200",
    },
  },
};
</script>

<style>
.card-img-top {
  max-width: 300px;
}
.card:hover {
  transform: scale(1.1);
  transition: transform 0.5s;
  z-index: 1;
}

.card {
  max-width: 300px;
  border-radius: 8px;
  box-shadow: 0 13px 27px -5px hsla(240, 30.1%, 28%, 0.25),
    0 8px 16px -8px hsla(0, 0%, 0%, 0.3), 0 -6px 16px -6px hsla(0, 0%, 0%, 0.03);
  transition: transform 0.2s;
}
</style>
