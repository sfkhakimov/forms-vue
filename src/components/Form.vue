<template>
  <div>
    <h1>Заполните форму</h1>
    <form class="form" @submit.prevent="submitForm" novalidate="true">
      {{ Object.keys(this.about).map(elem => {
      if (elem.type === 'text') {
        console.log(elem)
        return <FormInput

        />
        <FormChecked />
        <FormSelect />
      }
      })}}
      <!-- <FormInput
        :label="about.lastName.label"
        v-model="about.lastName.value"
        :required="about.lastName.required"
        :touched="about.lastName.touched"
        :placeholder="about.lastName.placeholder"
        :errorText="about.lastName.errorText"
        @input="handleValidate(about.lastName)"
      />
      <FormInput
        :label="about.firstName.label"
        v-model="about.firstName.value"
        :required="about.firstName.required"
        :touched="about.firstName.touched"
        :placeholder="about.firstName.placeholder"
        :errorText="about.firstName.errorText"
        @input="handleValidate(about.firstName)"
      />
      <FormInput
        :label="about.middleName.label"
        v-model="about.middleName.value"
        :required="about.middleName.required"
        :touched="about.middleName.touched"
        :placeholder="about.middleName.placeholder"
        @input="handleValidate(about.middleName)"
      />
      <FormInput
        :label="about.dateOfBirth.label"
        v-model="about.dateOfBirth.value"
        :required="about.dateOfBirth.required"
        :touched="about.dateOfBirth.touched"
        :type="about.dateOfBirth.type"
        :errorText="about.dateOfBirth.errorText"
        @input="handleValidate(about.dateOfBirth)"
      />
      <FormInput
        :label="about.phoneNumber.label"
        v-model="about.phoneNumber.value"
        :required="about.phoneNumber.required"
        :touched="about.phoneNumber.touched"
        :placeholder="about.phoneNumber.placeholder"
        :name="about.phoneNumber.name"
        :errorText="about.phoneNumber.errorText"
        @input="handleValidate(about.phoneNumber)"
      />
      <FormChecked
        :label="about.sex.label"
        v-model="about.sex.value"
        :name="about.sex.name"
        :type="about.sex.type"
        :initialValue="about.sex.initialValue"
        @input="handleValidate(about.sex)"
      />
      <FromSelect
        :label="about.customerGroup.label"
        v-model="about.customerGroup.value"
        :required="about.customerGroup.required"
        :touched="about.customerGroup.touched"
        :placeholder="about.customerGroup.placeholder"
        :initialValue="about.customerGroup.initialValue"
        :multiple="about.customerGroup.multiple"
        :errorText="about.customerGroup.errorText"
        @input="handleValidate(about.customerGroup)"
      />
      <FromSelect
        :label="about.attendingDoctor.label"
        v-model="about.attendingDoctor.value"
        :touched="about.attendingDoctor.touched"
        :placeholder="about.attendingDoctor.placeholder"
        :initialValue="about.attendingDoctor.initialValue"
        @input="handleValidate(about.attendingDoctor)"
      />
      <FormInput
        :label="about.sms.label"
        v-model="about.sms.value"
        :type="about.sms.type"
        :required="about.sms.required"
        :touched="about.sms.touched"
        @input="handleValidate(about.sms)"
      />-->
      <h2>Адрес</h2>

      <FormInput
        :label="address.index.label"
        v-model="address.index.value"
        @input="handleValidate(address.index)"
      />
      <FormInput
        :label="address.country.label"
        v-model="address.country.value"
        @input="handleValidate(address.country)"
      />
      <FormInput
        :label="address.region.label"
        v-model="address.region.value"
        @input="handleValidate(address.region)"
      />
      <FormInput
        :label="address.city.label"
        v-model="address.city.value"
        :required="address.city.required"
        :touched="address.city.touched"
        :errorText="address.city.errorText"
        @input="handleValidate(address.city)"
      />
      <FormInput
        :label="address.street.label"
        v-model="address.street.value"
        @input="handleValidate(address.street)"
      />
      <FormInput
        :label="address.house.label"
        v-model="address.house.value"
        @input="handleValidate(address.house)"
      />

      <h2>Документ</h2>
      <FromSelect
        :label="document.typeDocument.label"
        v-model="document.typeDocument.value"
        :touched="document.typeDocument.touched"
        :initialValue="document.typeDocument.initialValue"
        :errorText="document.typeDocument.errorText"
        @input="handleValidate(document.typeDocument)"
      />
      <FormInput
        :label="document.series.label"
        v-model="document.series.value"
        @input="handleValidate(document.series)"
      />
      <FormInput
        :label="document.item.label"
        v-model="document.item.value"
        @input="handleValidate(document.item)"
      />
      <FormInput
        :label="document.issuedBy.label"
        v-model="document.issuedBy.value"
        @input="handleValidate(document.issuedBy)"
      />
      <FormInput
        :label="document.dateOfIssue.label"
        v-model="document.dateOfIssue.value"
        :type="document.dateOfIssue.type"
        @input="handleValidate(document.dateOfIssue)"
      />
      <button :disabled="validForm()">Отправить</button>
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
      about: {
        lastName: {
          type: "text",
          label: "Фамилия*",
          value: "",
          touched: false,
          required: true,
          placeholder: "Введите Фамилию",
          errorText: "",
          isValid: false,
        },
        firstName: {
          type: "text",
          label: "Имя*",
          value: "",
          touched: false,
          required: true,
          placeholder: "Введите Имя",
          errorText: "",
          isValid: false,
        },
        middleName: {
          type: "text",
          label: "Отчество",
          value: "",
          touched: false,
          required: false,
          placeholder: "Введите Отчество",
          isValid: true,
        },
        dateOfBirth: {
          label: "Дата рождения*",
          value: "",
          touched: false,
          required: false,
          placeholder: "Введите дату рождения",
          type: "date",
          errorText: "",
          isValid: false,
        },
        phoneNumber: {
          type: "text",
          label: "Номер телефона*",
          value: "",
          touched: false,
          required: true,
          placeholder: "Введите номер телефона",
          name: "phone",
          errorText: "",
          isValid: false,
        },
        sex: {
          label: "Выберете пол",
          value: "",
          name: "radio",
          type: "radio",
          initialValue: [
            { value: "М", text: "М", id: 1 },
            { value: "Ж", text: "Ж", id: 2 },
          ],
          isValid: true,
        },
        customerGroup: {
          type: "select",
          label: "Группа клиентов*",
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
          label: "Лечащий врач",
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
          label: "Не отправлять СМС",
          value: false,
          required: false,
          touched: false,
          type: "checkbox",
          errorText: "",
          isValid: true,
        },
      },
      address: {
        index: {
          label: "Индекс",
          value: "",
          isValid: true,
        },
        country: {
          label: "Страна",
          value: "",
          isValid: true,
        },
        region: {
          label: "Область",
          value: "",
          isValid: true,
        },
        city: {
          required: true,
          value: "",
          label: "Город*",
          touched: false,
          errorText: "",
          isValid: false,
        },
        street: {
          label: "Улица",
          value: "",
          isValid: true,
        },
        house: {
          label: "Дом",
          value: "",
          isValid: true,
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
          label: "Тип документа*",
        },
        series: {
          label: "Серия",
          value: "",
          isValid: true,
        },
        item: {
          label: "Номер",
          value: "",
          isValid: true,
        },
        issuedBy: {
          label: "Кем выдан",
          value: "",
          isValid: true,
        },
        dateOfIssue: {
          label: "Дата выдачи",
          value: "",
          type: "date",
          isValid: true,
        },
      },
    };
  },
  methods: {
    submitForm() {
      const data = { ...this.about, ...this.address, ...this.document };
      console.log(data);
    },
    handleValidate(data) {
      console.log(data.value);
      let error = false;
      data.touched = true;
      data.isValid = true;
      data.errorText = "";
      const regExp = /^((\+7)|(8))\s?((\([0-9]{3}\))|([0-9]{3}))\s?-?[0-9]{3}-?[0-9]{2}-?[0-9]{2}/;
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

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 400px;
  margin: 0 auto;
  border: 1px solid gray;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 40px;
}

.form__label {
  padding-bottom: 2px;
  margin-top: 8px;
}
button {
  margin-top: 10px;
}
</style>