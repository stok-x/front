<template>
    <div id="intro" class="bg-image shadow-2-strong">
      <div class="mask d-flex align-items-center h-100" style="background-color: rgba(0, 0, 0, 0.8);">
        <div class="container">
          <div class="row justify-content-center">
            <div class="col-xl-5 col-md-8">
              <slot></slot>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<style>
#intro {
  background-image: url(https://mdbootstrap.com/img/new/fluid/city/008.jpg);
  height: 100vh;
}

</style>
<script>

export default {
  components: {}
}
</script>