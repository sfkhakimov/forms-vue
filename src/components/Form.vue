<template>
  <div>
    <h1>Заполните форму</h1>
    <form class="form" @submit.prevent="submitForm" novalidate="true">
      <div v-for="elem in Object.values(about)" :key="elem.label">
        <template
          v-if="
            elem.type === 'text' ||
              elem.type === 'date' ||
              elem.type === 'checkbox'
          "
        >
          <FormInput
            :label="elem.label"
            :type="elem.type"
            v-model="elem.value"
            :required="elem.required"
            :touched="elem.touched"
            :placeholder="elem.placeholder"
            :errorText="elem.errorText"
            @input="handleValidate(elem)"
          />
        </template>
        <template v-if="elem.type === 'radio'">
          <FormChecked
            :label="elem.label"
            v-model="elem.value"
            :required="elem.required"
            :touched="elem.touched"
            :name="elem.name"
            :type="elem.type"
            :initialValue="elem.initialValue"
            @input="handleValidate(elem)"
          />
        </template>
        <template v-if="elem.type === 'select'">
          <FromSelect
            :label="elem.label"
            v-model="elem.value"
            :required="elem.required"
            :touched="elem.touched"
            :initialValue="elem.initialValue"
            :multiple="elem.multiple"
            :errorText="elem.errorText"
            @input="handleValidate(elem)"
          />
        </template>
      </div>
      <hr class="form__separator" />
      <h2 class="form__title">Адрес</h2>
      <div v-for="elem in Object.values(address)" :key="elem.label">
        <FormInput
          :label="elem.label"
          v-model="elem.value"
          :required="elem.required"
          :touched="elem.touched"
          :errorText="elem.errorText"
          :placeholder="elem.placeholder"
          @input="handleValidate(elem)"
        />
      </div>
      <hr class="form__separator" />
      <h2 class="form__title">Документ</h2>
      <div v-for="elem in Object.values(document)" :key="elem.label">
        <template v-if="elem.type === 'select'">
          <FromSelect
            :type="elem.type"
            :label="elem.label"
            v-model="elem.value"
            :touched="elem.touched"
            :required="elem.required"
            :initialValue="elem.initialValue"
            :errorText="elem.errorText"
            @input="handleValidate(elem)"
          />
        </template>
        <template v-else-if="elem.type === 'date'">
          <FormInput
            :label="elem.label"
            :type="elem.type"
            v-model="elem.value"
            :required="elem.required"
            :touched="elem.touched"
            :errorText="elem.errorText"
            @input="handleValidate(elem)"
          />
        </template>
        <template v-else>
          <FormInput
            :label="elem.label"
            v-model="elem.value"
            :placeholder="elem.placeholder"
            @input="handleValidate(elem)"
          />
        </template>
      </div>
      <button class="form__button" :disabled="validForm()">Отправить</button>
      <span class="form__success" v-if="userRegistered">Клиент зарегистрирован</span>
    </form>
  </div>
</template>

<script>
import FormInput from "./FormInput";
import FromSelect from "./FormSelect";
import FormChecked from "./FormChecked";

export default {
  data() {
    return {
      userRegistered: false,
      about: {
        lastName: {
          type: "text",
          label: "Фамилия:*",
          value: "",
          touched: false,
          required: true,
          placeholder: "Введите Фамилию",
          errorText: "",
          isValid: false,
        },
        firstName: {
          type: "text",
          label: "Имя:*",
          value: "",
          touched: false,
          required: true,
          placeholder: "Введите Имя",
          errorText: "",
          isValid: false,
        },
        middleName: {
          type: "text",
          label: "Отчество:",
          value: "",
          touched: false,
          required: false,
          placeholder: "Введите Отчество",
          isValid: true,
        },
        dateOfBirth: {
          label: "Дата рождения:*",
          value: "",
          touched: false,
          required: false,
          type: "date",
          errorText: "",
          isValid: false,
        },
        phoneNumber: {
          type: "text",
          label: "Номер телефона:*",
          value: "",
          touched: false,
          required: true,
          placeholder: "В формате +79876543210",
          name: "phone",
          errorText: "",
          isValid: false,
        },
        sex: {
          label: "Выберете пол:",
          value: "",
          name: "radio",
          type: "radio",
          initialValue: [
            { value: "М", text: "М", id: 1 },
            { value: "Ж", text: "Ж", id: 2 },
          ],
          isValid: true,
          required: false,
          touched: false,
        },
        customerGroup: {
          type: "select",
          label: "Группа клиентов:*",
          value: [],
          touched: false,
          required: true,
          multiple: true,
          errorText: "",
          isValid: false,
          initialValue: [
            { value: "VIP", text: "VIP", id: 1 },
            { value: "Проблемные", text: "Проблемные", id: 2 },
            { value: "ОМС", text: "ОМС", id: 3 },
          ],
        },
        attendingDoctor: {
          type: "select",
          label: "Лечащий врач:",
          value: "",
          touched: false,
          required: false,
          multiple: false,
          errorText: "",
          isValid: true,
          initialValue: [
            { value: "Иванов", text: "Иванов", id: 1 },
            { value: "Захаров", text: "Захаров", id: 2 },
            { value: "Чернышева", text: "Чернышева", id: 3 },
          ],
        },
        sms: {
          label: "Не отправлять СМС:",
          value: false,
          required: false,
          touched: false,
          type: "checkbox",
          isValid: true,
        },
      },
      address: {
        index: {
          label: "Индекс:",
          value: "",
          isValid: true,
          placeholder: "Введите индекс",
        },
        country: {
          label: "Страна:",
          value: "",
          isValid: true,
          placeholder: "Введите страну",
        },
        region: {
          label: "Область:",
          value: "",
          isValid: true,
          placeholder: "Введите регион",
        },
        city: {
          required: true,
          value: "",
          label: "Город:*",
          touched: false,
          errorText: "",
          isValid: false,
          placeholder: "Введите город",
        },
        street: {
          label: "Улица:",
          value: "",
          isValid: true,
          placeholder: "Введите улицу",
        },
        house: {
          label: "Дом:",
          value: "",
          isValid: true,
          placeholder: "Введите дом",
        },
      },
      document: {
        typeDocument: {
          initialValue: [
            { value: "Паспорт", text: "Паспорт", id: 1 },
            {
              value: "Свидетельство о рождении",
              text: "Свидетельство о рождении",
              id: 2,
            },
            { value: "Вод. удостоверение", text: "Вод. удостоверение", id: 3 },
          ],
          required: true,
          value: "",
          touched: false,
          errorText: "",
          isValid: false,
          label: "Тип документа:*",
          type: "select",
        },
        series: {
          label: "Серия:",
          value: "",
          isValid: true,
          placeholder: "Введите серию документа",
        },
        item: {
          label: "Номер:",
          value: "",
          isValid: true,
          placeholder: "Введите номер документа",
        },
        issuedBy: {
          label: "Кем выдан:",
          value: "",
          isValid: true,
          placeholder: "Введите кем выдан документ",
        },
        dateOfIssue: {
          label: "Дата выдачи:*",
          value: "",
          type: "date",
          isValid: false,
          placeholder: "Введите дату выдачи",
          touched: false,
          required: true,
          errorText: "",
        },
      },
    };
  },
  methods: {
    submitForm() {
      const data = { ...this.about, ...this.address, ...this.document };
      this.userRegistered = true;
      Object.values(this.about).forEach((elem) => {
        if (elem.required === true) {
          elem.isValid = false;
        }
        if (elem.multiple === true) {
          elem.value = [];
        }
        if (elem.type === "checkbox") {
          elem.value = false;
        }
        elem.value = "";
      });
      Object.values(this.address).forEach((elem) => {
        if (elem.required === true) {
          elem.isValid = false;
        }
        elem.value = "";
      });
      Object.values(this.document).forEach((elem) => {
        if (elem.required === true) {
          elem.isValid = false;
        }
        elem.value = "";
      });
      return console.log(data);
    },
    handleValidate(data) {
      let error = false;
      this.userRegistered = false;
      data.touched = true;
      data.isValid = true;
      data.errorText = "";
      const regExp = /^((\+7)|(8))[0-9]{10}$/;
      if (
        data.required === true &&
        data.touched === true &&
        (data.value === "" || data.value.length === 0) &&
        error === false
      ) {
        error = true;
        data.errorText = "Это поле обязательно для заполнения";
        data.isValid = false;
      }
      if (
        data.required === true &&
        data.touched === true &&
        regExp.test(data.value) === false &&
        error === false &&
        data.name === "phone"
      ) {
        error = true;
        data.errorText = "Поле заполнено некорректно";
        data.isValid = false;
      }
    },
    validForm() {
      const about = Object.values(this.about).every((elem) => {
        return elem.isValid === true;
      });
      const address = Object.values(this.address).every((elem) => {
        return elem.isValid === true;
      });
      const document = Object.values(this.document).every((elem) => {
        return elem.isValid === true;
      });
      if (about && address && document) {
        return false;
      }
      return true;
    },
  },
  components: {
    FormInput,
    FromSelect,
    FormChecked,
  },
};
</script>

<style lang="scss" scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 320px;
  margin: 0 auto;
  border: 1px solid gray;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 40px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);

  &__button {
    margin-top: 10px;
    cursor: pointer;
  }

  &__title {
    margin: 0;
  }

  &__separator {
    width: 100%;
  }

  &__success {
    color: #228b22;
    padding-top: 10px;
    font-size: 14px;
  }
}
</style>
