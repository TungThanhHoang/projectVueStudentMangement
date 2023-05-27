<template>
  <div id="app">
    <NotifyModal v-if="showNotify" :status="setStatusNotify" />
    <StudentViewModal
      v-if="showStudentView"
      @handle-student-model="studentViewModal"
      :studentData="studentData"
      @handle-delete-student="deleteStudent"
      @handle-open-form-update="openFormUpdateStudent"
    />
    <FormInput :studentModel="studentModel" @handle-add-student="addStudent" />
    <div class="outline-wrapper">
      <hr />
    </div>
    <DashboardStudent
      :students="students"
      @handle-show-student-modal="studentViewModal"
      @handle-get-student-modal="getStudentModal"
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
      studentData: {},
      studentModel: {
        name: "",
        birthday: "",
        phone: "",
        gender: "",
        city: "",
        district: "",
        ward: "",
        address: "",
        isGraduate: false,
        nameUniversity: "",
        yearGraduate: 0,
        Gpa: 0,
      },
      statusNotify: {
        success_add_student: "success_add_student",
        error_add_student: "error_add_student",
        success_update_add_student: "success_update_add_student",
        error_update_add_student: "error_update_add_student",
      },
      setStatusNotify: "",
      students: [
        {
          id: "123",
          name: "Tung",
          birthday: "10/02/2000",
          phone: "012345678",
          gender: "Nam",
          city: "Hà Nội",
          district: "Hà Nội",
          ward: "Hà Nội",
          address: "abc",
          isGraduate: true,
          nameUniversity: "Bách Khoa",
          yearGraduate: 2023,
          Gpa: 3.14,
        },
        {
          id: "456",
          name: "Trương Quang Tân",
          birthday: "10/02/2000",
          phone: "012345678",
          gender: "Nam",
          city: "Hà Nội",
          district: "Hà Nội",
          ward: "Hà Nội",
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

    getStudentModal: function (student) {
      this.studentData = student;
    },

    addStudent: function (student) {
      console.log(student.id);
      const {
        id,
        name,
        phone,
        birthday,
        city,
        district,
        ward,
        address,
        gender,
      } = student;
      if (
        name === "" ||
        phone === "" ||
        birthday === "" ||
        city === "" ||
        district === "" ||
        ward === "" ||
        address === "" ||
        gender === ""
      ) {
        this.setStatusNotify = this.statusNotify.error_add_student;
        this.notifyModal(true),
          setTimeout(() => {
            this.notifyModal(false);
          }, 3000);
        return;
      }

      if (id) {
        const findIndex = this.students.findIndex((item) => item.id === id);
        if (findIndex !== -1) {
          const updateStudent = this.students[findIndex];
          updateStudent.name = name;
          updateStudent.birthday = birthday;
          updateStudent.phone = phone;
          updateStudent.gender = gender;
          updateStudent.city = city;
          updateStudent.district = district;
          updateStudent.ward = ward;

          this.setStatusNotify = this.statusNotify.success_update_add_student;
          this.notifyModal(true),
            setTimeout(() => {
              this.notifyModal(false);
            }, 3000);
        }
        return;
      }

      this.setStatusNotify = this.statusNotify.success_add_student;
      this.students.unshift({ id: new Date().toISOString(), ...student });
      this.notifyModal(true),
        setTimeout(() => {
          this.notifyModal(false);
        }, 3000);
    },
    deleteStudent: function (idStudent) {
      this.students = this.students.filter((item) => item.id !== idStudent);
      this.studentData = {};
      this.studentViewModal(false);
    },
    openFormUpdateStudent: function (Student) {
      this.studentModel = Student;
    },
  },
  watch: {
    students: {
      handler: function() {
        this.studentModel = {}
      },
      deep: true
    }
  }
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
