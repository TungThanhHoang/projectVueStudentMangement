<template>
  <div class="overlay">
    <div class="student-view-wrapper">
      <span class="title-header">Thông tin sinh viên</span>
      <span class="btn-close" @click="handleClickStudent()">X</span>
      <div class="outline-wrapper">
        <hr />
      </div>
      <div class="card-row">
        <div class="card-item">
          <span>Họ và tên:</span>
          <span>{{ studentData.name }}</span>
        </div>
        <div class="card-item">
          <span>Ngày sinh:</span>
          <span>{{ studentData.birthday }}</span>
        </div>
      </div>
      <div class="card-row">
        <div class="card-item">
          <span>Số điện thoại:</span>
          <span>{{ studentData.phone }}</span>
        </div>
        <div class="card-item">
          <span>Giới tính:</span>
          <span>{{ studentData.gender }}</span>
        </div>
      </div>
      <div class="card-row">
        <div class="card-item">
          <span>Thành phố:</span>
          <span>{{ studentData.city }}</span>
        </div>
        <div class="card-item">
          <span>Quận/huyện:</span>
          <span>{{ studentData.district }}</span>
        </div>
      </div>
      <div class="card-row">
        <div class="card-item">
          <span>Phường/xã:</span>
          <span>{{ studentData.ward }}</span>
        </div>
        <div class="card-item">
          <span>Địa chỉ:</span>
          <span>{{ studentData.address }}</span>
        </div>
      </div>
      <div class="card-row">
        <div class="card-item">
          <span>Trạng thái tốt nghiệp:</span>
          <span v-if="studentData.isGraduate">Đã tốt nghiệp</span>
          <span v-else>Chưa tốt nghiệp</span>
        </div>
        <template>
          <div class="card-item">
            <span>Tên trường:</span>
            <span v-if="studentData.nameUniversity">{{ studentData.nameUniversity }}</span>
            <span v-else>N/A</span>
          </div>
        </template>
      </div>
      <div class="card-row">
        <div class="card-item">
          <span>Năm tốt nghiệp:</span>
          <span v-if="studentData.yearGraduate">{{ studentData.yearGraduate }}</span>
          <span v-else>N/A</span>
        </div>
        <div class="card-item">
          <span>Điểm Gpa:</span>
          <span v-if="studentData.Gpa" >{{ studentData.Gpa }}</span>
          <span v-else >N/A</span>
        </div>
      </div>
      <div class="button-wrapper">
        <button @click="handleOpenFormUpdate">Cập nhật</button>
        <button @click="handleDeleteStudent">Xóa</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    status: String,
    studentData: Object,
  },
  methods: {
    handleClickStudent: function () {
      this.$emit("handle-student-model", false);
    },
    handleDeleteStudent: function() {
      this.$emit("handle-delete-student", this.studentData.id)
    },
    handleOpenFormUpdate: function() {
      this.$emit("handle-open-form-update", this.studentData)
      this.$emit("handle-student-model", false);
    }
  },
};
</script>

<style lang="scss">
$color-button: #2a7f62;
.overlay {
  background-color: rgba(149, 157, 165, 0.2);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 100;
  .student-view-wrapper {
    width: 600px;
    height: 360px;
    position: relative;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    padding: 25px;
    box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
    z-index: 100;
    background-color: #fff;
    font-size: 15px;
    border-radius: 8px;
    .outline-wrapper {
      margin: 30px 0 18px 0 !important;
    }
    .title-header {
      margin-top: 50px;
      font-size: 16px;
      font-weight: 600;
    }
    h4 {
      margin: 0;
    }
    .btn-close {
      position: absolute;
      right: 30px;
      top: 30px;
      cursor: pointer;
    }
    .card-row {
      display: flex;
      justify-content: space-between;
      margin-top: 18px;
      .card-item {
        display: flex;
        span:first-child {
          padding-right: 10px;
        }
      }
    }
    .button-wrapper {
      margin-top: 20px;
      button {
        border: none;
        padding: 10px 30px;
        background-color: #F58549;
        color: #fff;
        border-radius: 4px;
        cursor: pointer;
        &:hover {
          opacity: .8;
        }
        &:last-child {
          margin-left: 10px;
          background-color: #A50104;
        }
      }
    }
  }
}
</style>
