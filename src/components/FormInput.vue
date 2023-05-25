<template>
  <div class="form-wrapper">
    <form action="" class="form-control">
      <div class="form-row">
        <div class="form-input">
          <label for="name">Họ và tên</label>
          <input type="text" v-model="name" />
        </div>
        <div class="form-input">
          <label for="birthday">Ngày Sinh</label>
          <input type="date" v-model="birthday" />
        </div>
        <div class="form-input">
          <label for="phone">Số điện thoại</label>
          <input type="text" v-model="phone" />
        </div>
        <div class="form-input form-input-gender">
          <label for="phone">Giới tính</label>
          <div class="form-gender-wrapper">
            <div class="form-select-gender">
              <label for="male">Nam</label>
              <input type="radio" name="gender" value="Nam" v-model="gender" />
            </div>
            <div class="form-select-gender">
              <label for="female">Nữ</label>
              <input type="radio" name="gender" value="Nữ" v-model="gender" />
            </div>
          </div>
        </div>
      </div>
      <div class="form-row">
        <div class="form-input">
          <label for="text">Thành phố</label>
          <select v-model="city">
            <option value="Hà Nội">Hà Nội</option>
            <option value="Đà Nẵng">Đà Nẵng</option>
          </select>
        </div>
        <div class="form-input">
          <label for="text">Quận/Huyện</label>
          <select v-model="district">
            <option value="Hà nội">Hà Nội</option>
            <option value="Đà Nẵng">Đà Nẵng</option>
          </select>
        </div>
        <div class="form-input">
          <label for="text">Phường/Xã</label>
          <select v-model="ward">
            <option value="Hà nội">Hà Nội</option>
            <option value="Đà Nẵng">Đà Nẵng</option>
          </select>
        </div>
        <div class="form-input">
          <label for="text">Số nhà</label>
          <input type="text" v-model="address" />
        </div>
      </div>
      <div class="form-row">
        <div class="form-input">
          <div>
            <div class="form-select-radio">
              <div class="form-select-checkbox">
                <input type="checkbox" v-model="isGraduate" />
                <label for="">Đã tốt nghiệp</label>
              </div>
              <template v-if="isGraduate">
                <div class="option-checkbox">
                  <div class="form-input">
                    <label for="text">Tên trường</label>
                    <input type="text" v-model="nameUniversity" />
                  </div>
                  <div class="form-graduate-number">
                    <div class="form-input">
                      <label for="text">Năm tốt nghiệp</label>
                      <input type="text" v-model="yearGraduate" />
                    </div>
                    <div class="form-input">
                      <label for="text">GPA</label>
                      <input type="text" v-model="Gpa" />
                    </div>
                  </div>
                </div>
              </template>
            </div>
          </div>
        </div>
      </div>
      <button
        type="submit"
        class="button-submit-form"
        @click.prevent="
          addStudent({
            name,
            birthday,
            phone,
            gender,
            city,
            district,
            ward,
            address,
            isGraduate,
            nameUniversity,
            yearGraduate,
            Gpa
          })
        "
      >
        Lưu
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "FormInput",
  data() {
    return {
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
    };
  },
  props: {
    students: Array,
    addStudent: Function,
  },
};
</script>

<style lang="scss">
$color-text: #00072d;
$color-text-light: #a5a5a5;
$color-input-error: #fe5f55;
$color-input: #eee;
$color-button: #2a7f62;
.form-wrapper {
  margin: 0 auto;
  width: 800px;
  .form-control {
    margin: 0 auto;
    .form-row {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      row-gap: 10px;
      column-gap: 40px;
      margin-top: 20px;
      .form-input-gender {
        justify-content: flex-end;
      }
      .form-input {
        display: flex;
        flex-direction: column;
        margin-top: 8px;
        label {
          margin-bottom: 5px;
          font-size: 14px;
          font-weight: 500;
          color: $color-text;
        }
        input {
          height: 30px;
          outline: none;
          border: 1px solid $color-input;
          border-radius: 4px;
          padding: 2px 10px;
          &:focus {
            border-color: #000;
          }
        }
        select {
          height: 35px;
          outline: none;
          border: 1px solid $color-input;
          border-radius: 4px;
          padding: 2px 8px;
        }
        .form-gender-wrapper {
          display: flex;
          .form-select-gender {
            display: flex;
            align-items: flex-end;
            margin-right: 12px;
            label {
              margin: 0 4px 0 10px;
            }
            input {
              width: 18px;
              height: 18px;
            }
          }
        }
        .form-select-radio {
          display: flex;
          flex-direction: column;
          .form-select-checkbox {
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            label {
              margin: 2px 0 0 0;
            }
            input {
              width: 18px;
              height: 18px;
              margin-right: 10px;
            }
          }
          .option-checkbox {
            .form-graduate-number {
              margin-top: 10px;
              display: flex;
              flex-direction: row;
              justify-content: space-between;
            }
          }
        }
      }
    }
  }
  .button-submit-form {
    margin-top: 30px;
    width: 200px;
    height: 35px;
    outline: none;
    border: none;
    border-radius: 4px;
    color: #fff;
    font-weight: 600;
    font-size: 14px;
    background-color: $color-button;
    cursor: pointer;
    &:hover {
      opacity: 0.8;
    }
  }
}
</style>
