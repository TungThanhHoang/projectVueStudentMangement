<template>
  <div
    class="notify-wrapper"
    :style="{
      color:
        (status === statusNotify[success_add_student])
        | statusNotify[success_update_add_student]
          ? '#2a7f62'
          : 'red',
    }"
  >
    <h4>{{ showStatusNotify(status) }}</h4>
  </div>
</template>

<script>
export default {
  props: {
    status: String,
  },
  data() {
    return {
      statusNotify: {
        success_add_student: "Thêm thành công 🥳🥳🥳",
        error_add_student: "Thêm thất bại 😢😢😢",
        success_update_add_student: "Cập nhật thành công 🤓🤓🤓",
        error_update_add_student: "Cập nhật thất bại 😒😒😒",
      },
    };
  },
  methods: {
    showStatusNotify: function (status) {
      return this.statusNotify[status];
    },
  },
};
</script>

<style lang="scss">
$color-button: #2a7f62;
.notify-wrapper {
  margin: 0 auto;
  position: absolute;
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
}
</style>
