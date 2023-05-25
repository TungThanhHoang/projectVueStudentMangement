<template>
  <div class="overlay">
    <div class="student-view-wrapper">
        <span class="btn-close" @click="studentViewModal(false)">Close</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    status: String,
    studentViewModal: Function
  },
};
</script>

<style lang="scss">
$color-button: #2a7f62;
.overlay {
  background-color: rgba(149, 157, 165, 0.2);
//   width: 100%;
//   height: 100%;
//   position: fixed;
  .student-view-wrapper {
    width: 600px;
    height: 500px;
    position: fixed;
    left: 50%;
    transform: translateX(-50%);
    padding: 10px 40px;
    box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
    z-index: 100;
    background-color: #fff;
    font-size: 15px;
    h4 {
      margin: 0;
    }
    .btn-close {
        position: absolute;
        right: 20px;
        top: 20px;
        cursor: pointer;
    }
  }
}
</style>
