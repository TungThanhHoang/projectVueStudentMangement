<template>
  <div class="dashboard-wrapper">
    <h2>Dashboard Student</h2>
    <div class="table-dashboard">
      <div class="table-dashboard-header">
        <div class="table-header-item">Stt</div>
        <div class="table-header-item">Họ và tên</div>
        <div class="table-header-item">Ngày sinh</div>
        <div class="table-header-item">Số điện thoại</div>
        <div class="table-header-item">Giới tính</div>
        <div class="table-header-item">Thành phố</div>
        <div class="table-header-item">Quận/Huyện</div>
        <div class="table-header-item">Phường/Xã</div>
        <div class="table-header-item">Số nhà</div>
        <div class="table-header-item">Tốt nghiệp</div>
      </div>
      <div class="table-dashboard-body">
        <div
          class="table-dashboard-item"
          v-for="(item, index) in students"
          :key="index"
          @click="openStudentModal(item)"
        >
          <div>{{ index + 1 }}</div>
          <div>{{ item.name }}</div>
          <div>{{ item.birthday }}</div>
          <div>{{ item.phone }}</div>
          <div>{{ item.gender }}</div>
          <div>{{ item.city }}</div>
          <div>{{ item.district }}</div>
          <div>{{ item.ward }}</div>
          <div>{{ item.address }}</div>
          <div
            :class="[
              item.isGraduate ? status_graduate : status_not_graduate,
            ]"
          >
            {{ item.isGraduate ? "Đã tốt nghiệp" : "Chưa tốt nghiệp" }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    students: Array
  },
  data() {
    return {
        status_graduate: 'status-graduate',
        status_not_graduate: 'status-not-graduate'
    }
  },
  methods: {
    openStudentModal: function(item) {
      this.$emit('handle-get-student-modal', item);
      this.$emit('handle-show-student-modal', true);
    }
  }
};
</script>

<style lang="scss">
$color-text: #00072d;
$color-text-light: #a5a5a5;
$color-input-error: #fe5f55;
$color-input: #eee;
$color-button: #2a7f62;
.dashboard-wrapper {
  margin-top: 50px;
  h3 {
    color: $color-text;
    font-weight: 600;
  }
  .table-dashboard {
    margin-top: 20px;
    .table-dashboard-header {
      display: grid;
      text-align: center;
      grid-template-columns: repeat(10, 1fr);
      border: 1px solid #eee;
      padding: 18px 0;
      .table-header-item {
        border-right: 1px solid $color-input;
        &:last-child {
          border-right: unset;
        }
      }
    }
    .table-dashboard-body {
      margin-top: 10px;
      .table-dashboard-item {
        display: grid;
        text-align: center;
        grid-template-columns: repeat(10, 1fr);
        border: 1px solid #eee;
        border-width: 0 1px 1px 1px;
        padding: 15px 0;
        &:hover {
          opacity: 0.5;
        }
        &:first-child {
          border: 1px solid #eee;
        }
        div {
          text-overflow: ellipsis;
          overflow: hidden;
          white-space: nowrap;
          font-size: 13px;
          color: $color-text;
          cursor: pointer;
        }
        .status-graduate {
          border: 1px solid $color-button;
          padding: 6px;
          border-radius: 50px;
          width: 75%;
          justify-self: center;
          color: green;
        }
        .status-not-graduate {
          border: 1px solid red;
          padding: 6px;
          border-radius: 50px;
          justify-self: center;
          color: red;
        }
      }
    }
  }
}
</style>
