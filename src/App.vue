<template>
  <div id="app">
    <NotifyModal v-if="showNotify" :status="setStatusNotify" />
    <StudentViewModal v-if="showStudentView" :studentViewModal="studentViewModal" />
    <FormInput :students="students" :addStudent="addStudent" />
    <div class="outline-wrapper">
      <hr />
    </div>
    <DashboardStudent
      :students="students"
      :studentViewModal="studentViewModal"
    />
  </div>
</template>

<script>
import DashboardStudent from "./components/DashboardStudent.vue";
import FormInput from "./components/FormInput.vue";
import NotifyModal from "./components/NotifyModal.vue";
import StudentViewModal from "./components/StudentViewModal.vue";
export default {
  name: "App",
  components: {
    FormInput,
    DashboardStudent,
    NotifyModal,
    StudentViewModal,
  },
  data: function () {
    return {
      showNotify: false,
      showStudentView: false,
      statusNotify: {
        success_add_student: "success_add_student",
        error_add_student: "error_add_student",
        success_update_add_student: "success_update_add_student",
        error_update_add_student: "error_update_add_student",
      },
      setStatusNotify: "",
      students: [
        {
          name: "Tung",
          birthday: "10/02/2000",
          phone: "012345678",
          gender: "Nam",
          city: "Hà nội",
          district: "Hoàng Mai",
          ward: "Hải châu",
          address: "abc",
          isGraduate: true,
          nameUniversity: "Bách Khoa",
          yearGraduate: 2023,
          Gpa: 3.14,
        },
        {
          name: "Trương Quang Tân",
          birthday: "10/02/2000",
          phone: "012345678",
          gender: "Nam",
          city: "Hà nội",
          district: "Hoàng Mai",
          ward: "Hải châu",
          address: "abc",
          isGraduate: false,
          nameUniversity: "",
          yearGraduate: 0,
          Gpa: 0,
        },
      ],
    };
  },
  methods: {
    notifyModal: function (status) {
      this.showNotify = status;
    },

    studentViewModal: function (status) {
      this.showStudentView = status;
    },

    addStudent: function (student) {
      const { name, phone, birthday, city, district, ward, address } = student;
      if (
        name === "" ||
        phone === "" ||
        birthday === "" ||
        city === "" ||
        district === "" ||
        ward === "" ||
        address === ""
      ) {
        this.setStatusNotify = this.statusNotify.error_add_student;
        this.notifyModal(true),
          setTimeout(() => {
            this.notifyModal(false);
          }, 3000);
        return;
      }
      this.setStatusNotify = this.statusNotify.success_add_student;
      this.students.push(student);
      this.notifyModal(true),
        setTimeout(() => {
          this.notifyModal(false);
        }, 3000);
    },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  html {
    margin: 0;
    padding: 0;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    width: 1200px;
    margin: 0 auto;
    .outline-wrapper {
      margin: 50px 0;
      hr {
        border: 1px dashed #eee;
      }
    }
  }
}
</style>
