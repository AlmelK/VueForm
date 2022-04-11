<template>
  <div class="root">
    <div class="title">Регистрация</div>
    <form class="sign-up" @submit.prevent="submitHandler">
      <div class="personal-info">
        <div class="title2">Личные данные</div>
        <div class="form-group">
          <label for="surName">Фамилия</label>
          <input
            type="text"
            id="surName"
            v-model.trim="formData.surname"
            placeholder="Введите вашу фамилию"
            :class="{invalid: ($v.formData.surname.$dirty && !$v.formData.surname.required) ||($v.formData.surname.$dirty && !$v.formData.surname.minLength) || ($v.formData.surname.$dirty && !$v.formData.surname.alpha)}"
          />
          <small class="helper-text"
          v-if="$v.formData.surname.$dirty && !$v.formData.surname.required">Поле не должно быть пустым</small>
          <small class="helper-text"
          v-else-if="$v.formData.surname.$dirty && !$v.formData.surname.minLength">Слишком короткое значение</small>
          <small class="helper-text"
          v-else-if="$v.formData.surname.$dirty && !$v.formData.surname.alpha">Фамилия должна начинаться с большой буквы</small>

        </div>
        <div class="form-group">
          <label for="name">Имя</label>
          <input
            type="text"
            id="name"
            v-model="formData.clientName"
            placeholder="Введите ваше имя"
            :class="{invalid: ($v.formData.clientName.$dirty && !$v.formData.clientName.required) ||($v.formData.clientName.$dirty && !$v.formData.clientName.minLength) || ($v.formData.clientName.$dirty && !$v.formData.clientName.alpha)}"
          />
          <small class="helper-text"
          v-if="$v.formData.clientName.$dirty && !$v.formData.clientName.required">Поле не должно быть пустым</small>
          <small class="helper-text"
          v-else-if="$v.formData.clientName.$dirty && !$v.formData.clientName.minLength">Слишком короткое значение</small>
          <small class="helper-text"
          v-else-if="$v.formData.clientName.$dirty && !$v.formData.clientName.alpha">Имя должно начинаться с большой буквы</small>
        </div>
        <div class="form-group-not-important">
          <label for="third_name">Отчество</label>
          <input
            type="text"
            id="third_name"
            v-model="formData.thirdName"
            placeholder="Введите ваше отчество"
          />
        </div>
        <div class="form-group">
          <label for="birth_day">Дата рождения</label>
          <input 
          type="date" 
          id="birth_day" 
          v-model="formData.birthday"
          :class="{invalid: ($v.formData.birthday.$dirty && !$v.formData.birthday.required)}"
           />
           <small class="helper-text"
          v-if="$v.formData.birthday.$dirty && !$v.formData.birthday.required">Обязательно укажите дату рождения</small>
        </div>
        <div class="form-group">
          <label for="phone">Номер телефона</label>
          <input
            type="tel"
            id="phone"
            v-model="formData.phoneNumber"
            placeholder="Введите номер телефона"
            :class="{invalid: ($v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.required) || 
            ($v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.minLength) ||
            ($v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.maxLength) ||
            ($v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.alpha) }"
          />
          <small class="helper-text"
          v-if="$v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.required">Поле не должно быть пустым</small>
          <small class="helper-text"
          v-else-if="$v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.minLength">Минимум 11 цифр</small>
          <small class="helper-text"
          v-else-if="$v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.maxLength">Максимум 11 цифр</small>
          <small class="helper-text"
          v-else-if="$v.formData.phoneNumber.$dirty && !$v.formData.phoneNumber.alpha">Некорректный формат, попробуйте начать с 7</small>
        </div>

        <div class="gender-radio">
          <label class="label_gen" for="gender">Пол</label>
          <div id="gender">
            <input
              class="radio"
              type="radio"
              id="m"
              value="male"
              v-model="formData.gender"
            />
            <label for="m">М</label>

            <input
              class="radio"
              type="radio"
              id="f"
              value="female"
              v-model="formData.gender"
            />
            <label for="f">Ж</label>
          </div>
        </div>

        <div class="form-group">
          <label for="clientGroup">Группа клиентов</label>
          <select id="clientGroup" v-model="formData.selectedGroups" multiple>
            <option v-for="(g, index) in clientsGroup" :value="g" :key="index">
              {{ g.group }}
            </option>
          </select>
          <div class="selected-options">
            <div
              class="selected-opt"
              v-for="(selected, index) in formData.selectedGroups"
              :key="index"
            >
              {{ selected.group }}
            </div>
          </div>
        </div>

        <div class="form-group-not-important">
          <label for="doctorGroup">Лечащий врач</label>
          <select id="doctorGroup" v-model="formData.doctor">
            <option disabled value="">Выберите один из вариантов</option>
            <option v-for="(doc, index) in doctors" :value="doc" :key="index">
              {{ doc.doctorName }}
            </option>
          </select>
        </div>

        <div class="form-group-check">
          <input type="checkbox" id="sms" v-model="formData.notSendSMS" />
          <label for="sms">Не отправлять СМС.</label>
        </div>
      </div>

      <div class="adress-info">
        <div class="title2">Адрес</div>

        <div class="form-group-not-important">
          <label>Страна</label>
          <input type="text" v-model="formData.country" placeholder="Введите страну" />
        </div>

        <div class="form-group-not-important">
          <label>Область</label>
          <input type="text" v-model="formData.region" placeholder="Введите область" />
        </div>

        <div class="form-group">
          <label>Город</label>
          <input type="text" v-model="formData.city" placeholder="Введите город" />
        </div>

        <div class="form-group-not-important">
          <label>Улица</label>
          <input type="text" v-model="formData.street" placeholder="Введите адрес" />
        </div>

        <div class="form-group-two-fields">
          <div class="field-one">
            <label>Дом</label>
            <input type="text" v-model="formData.house" placeholder="Дом" />
          </div>

          <div class="field-two">
            <label>Индекс</label>
            <input type="text" v-model="formData.zipcode" placeholder="Индекс" />
          </div>
        </div>
      </div>

      <div class="passport_data">
        <div class="title2">Паспортные данные</div>

        <div class="form-group">
          <label>Тип документа</label>
          <select v-model="formData.documentType">
            <option disabled value="">Выберите один из вариантов</option>
            <option
              v-for="(document, index) in documentTypes"
              :key="index"
              :value="document"
            >
              {{ document.doctype }}
            </option>
          </select>
        </div>

        <div class="form-group-two-fields">
          <div class="field-one">
            <label>Серия</label>
            <input type="text" v-model="formData.passportSeries" placeholder="Серия" />
          </div>

          <div class="field-two">
            <label>Номер</label>
            <input type="text" v-model="formData.passportNumber" placeholder="Номер" />
          </div>
        </div>

        <div class="form-group-not-important">
          <label>Кем выдан</label>
          <input type="text" v-model="formData.issuedBy" placeholder="Введите адрес" />
        </div>

        <div class="form-group">
          <label for="issued_date">Дата выдачи</label>
          <input type="date" id="issued_date" v-model="formData.issuedDate" />
        </div>
      </div>
      <div class="send-button">
        <button type="submit">Отправить</button>
      </div>
    </form>
  </div>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, minLength, maxLength } from "vuelidate/lib/validators"

export default {
  mixins: [validationMixin],
  data() {
    return {
      formData: {
        surname: "",
        clientName: "",
        thirdName: "",
        birthday: [],
        phoneNumber: "",
        gender: "male",
        selectedGroups: [{ group: "ОМС", value: "OMS" }],
        doctor: [{ doctorName: "Иванов", value: "Ivanov" }],
        notSendSMS: false,
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
        zipcode: "",
        documentType: [
          {
            doctype: "Паспорт",
            value: "Passport",
          },
        ],
        passportSeries: "",
        passportNumber: "",
        issuedBy: "",
        issuedDate: [],
      },

      clientsGroup: [
        {
          group: "VIP",
          value: "VIP",
        },
        {
          group: "Проблемные",
          value: "Problem",
        },
        {
          group: "ОМС",
          value: "OMS",
        },
      ],
      doctors: [
        {
          doctorName: "Иванов",
          value: "Ivanov",
        },
        {
          doctorName: "Захаров",
          value: "Zaharov",
        },
        {
          doctorName: "Чернышева",
          value: "Chernisheva",
        },
      ],
      documentTypes: [
        {
          doctype: "Паспорт",
          value: "Passport",
        },
        {
          doctype: "Свидетельство о рождении",
          value: "BirthCertificate",
        },
        {
          doctype: "Вод. удостоверение",
          value: "DriveLicense",
        },
      ],
    };
  },
  validations: {
    formData: {
      surname: { 
        required, 
        minLength: minLength(4),
        alpha: val => /^[А-ЯA-Z]/.test(val)
        },
      clientName: {
        required, 
        minLength: minLength(3),
        alpha: val => /^[А-ЯA-Z]/.test(val)
      },
      birthday: {required},
      phoneNumber: {
        required, 
        minLength: minLength(11),
        maxLength: maxLength(11),
        alpha: val =>  /^7\d/.test(val)
      },
      selectedGroups:{ required },
      city: {
        required,
        minLength: minLength(3),
        alpha: val => /^[А-ЯA-Z]/.test(val)
      }
      },
      
    },
  methods: {
    submitHandler() {
      if(this.$v.$invalid){
        this.$v.$touch()
        console.log('Валидация прошла успешно')
        return
      }
    }
  }
  
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
$bottomPadTitle: 5px
%form-group-labels
  display: block
  font-size: 16px
  font-weight: 600
  margin-bottom: 5px
  color: #666

%important_fields
  content: "*"
  position: relative
  font-size: 18px
  color: red

@mixin input_forms($width_value)
  height: 40px
  width: $width_value
  outline: none
  border-radius: 5px
  border: 1px solid #ccc
  padding-left: 15px
  padding-right: 5px
  font-size: 16px
  border-bottom-width: 2px
  transition: all 0.3s ease

.root
  margin: 0 auto
  max-width: 90%
  background: #fff
  padding: 25px 30px
  border-radius: 15px
  box-shadow: 8px 8px 5px 2px #c0c0c0

  .title
    text-align: center
    font-size: 24px
    font-weight: 600
    padding-bottom: 15px

  .sign-up

    .title2
      font-size: 20px
      font-weight: 600
      padding-bottom: 5px

    .personal-info, .adress-info, .passport_data
      display: block
      justify-content: space-between
      margin-bottom: 25px

      .form-group-not-important
        margin: 15px 0 5px 0
        width: 100%
        color: #666

        label
          @extend %form-group-labels

        input, select
          @include input_forms(100%)

          &::placeholder
            color: #a8acc9

      .form-group-two-fields
        margin: 10px 0 5px 0
        display: flex
        width: 100%

        label
          @extend %form-group-labels

        .field-one
          margin-right: 50px

          input
            @include input_forms(100%)

            &::placeholder
              color: #a8acc9
        .field-two
          input
            @include input_forms(100%)

            &::placeholder
              color: #a8acc9

      .form-group
        margin: 20px 0 10px 0
        width: 100%
        
        .invalid
          border: 1px solid red
          transition: .2s
        
        .helper-text
          font-size: 12px
          color: red  

        label
          @extend %form-group-labels

          &:after
            @extend %important_fields

        input, select
          @include input_forms(100%)

          &::placeholder
            color: #a8acc9

      .gender-radio

        .label_gen
          font-size: 18px
          font-weight: 600
          color: #666


        #gender
          margin: 14px 0
          display: flex
          width: 100%
          justify-content: start

          label
            margin-right: 20px

          .radio
            width: 15px
            height: 15px
            margin-right: 10px

      #clientGroup
        height: 100px
        padding-top: 5px
        overflow-y: hidden

        option
          padding-bottom: 5px
          padding-top: 5px
          padding-left: 5px
          margin-right: 5px
          border-radius: 10px

      .selected-options
        display: flex
        flex-wrap: wrap
        padding: 8px 5px
        justify-content: start
        width: 100%

        .selected-opt
          padding: 8px 16px
          border-radius: 15px
          background: #e5e5e5
          margin-top: 5px
          margin-right: 10px

      .form-group-check
        margin-top: 10px
        display: flex

        input[type=checkbox]
          width: 18px
          height: 18px
          margin: 10px 5px
        label
          padding: 10px 5px

    .send-button
      width: 100%
      display: flex
      justify-content: center

      button
        width: 60%
        height: 40px
        border-radius: 15px
        border: 1px solid #ccc
        background: linear-gradient(to left, #fff, #fff 20%, #ccc 100%)
        font-weight: 600
        font-size: 18px
        color: #666
        cursor: pointer

        &:hover
          box-shadow: 5px 5px 2px 2px #ccc
          background: linear-gradient(to left, #ccc, #ccc 20%, #fff 100%)
          transition: .5s
</style>