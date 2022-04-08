<template>
  <div class="root">
    <div class="title">Регистрация</div>
    <form class="sign-up">
      <div class="title2">Личные данные</div>
      <div class="personal-info">
        <div class="form-group">
          <label for="surName">Фамилия</label>
          <input
            type="text"
            id="surName"
            v-model="surname"
            placeholder="Введите вашу фамилию"
          />
        </div>
        <div class="form-group">
          <label for="name">Имя</label>
          <input
            type="text"
            id="name"
            v-model="clientName"
            placeholder="Введите ваше имя"
          />
        </div>
        <div class="form-group-not-important">
          <label for="third_name">Отчество</label>
          <input
            type="text"
            id="third_name"
            v-model="thirdName"
            placeholder="Введите ваше отчество"
          />
        </div>
        <div class="form-group">
          <label for="birth_day">Дата рождения</label>
          <input
            type="date"
            id="birth_day"
            v-model="birthday"
            placeholder="Введите вашу дату рождения"
          />
        </div>
        <div class="form-group">
          <label for="phone">Номер телефона</label>
          <input
            type="tel"
            id="phone"
            v-model="phoneNumber"
            placeholder="Введите ваш номер телефона"
          />
        </div>

        <div class="gender-radio">
          <label class="label_gen" for="gender">Пол</label>
          <div id="gender">            
              <input
                class="radio"
                type="radio"
                id="m"
                value="male"
                v-model="gender"
              />
              <label for="m">М</label>            

              <input
                class="radio"
                type="radio"
                id="f"
                value="female"
                v-model="gender"
              />
              <label for="f">Ж</label>
          </div>
        </div>

        <div class="form-group">
          <label for="clientGroup">Группа клиентов</label>
          <select id="clientGroup" v-model="selectedGroups" multiple size="0">
            <option
              v-for="(g, index) in clientsGroup"
              :value="g.value"
              :key="index"
            >
              {{ g.group }}
            </option>            
          </select>
          <div class="selected-options">
              <div class="selected-opt" v-for="selected, index in selectedGroups" :key="index">{{selected}}</div>
          </div>
          
        </div>

        <div class="form-group">
          <label for="doctorGroup">Лечащий врач</label>
          <select id="doctorGroup" v-model="doctor">
            <option
              v-for="(doc, index) in doctors"
              :value="doc.value"
              :key="index"
            >
              {{ doc.doctorName }}
            </option>
          </select>
        </div>

        <div class="form-group-check">
          <input type="checkbox" id="sms" v-model="notSendSMS" />
          <label for="sms">Не отправлять СМС.</label>
        </div>
        
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      surname: "",
      clientName: "",
      thirdName: "",
      birthday: "",
      phoneNumber: "",
      gender: "male",
      selectedGroups: ["OMS"],
      doctor: "",
      notSendSMS: false,
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
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
$bottomPadTitle: 10px
%form-group-labels
  display: block
  font-size: 18px
  font-weight: 600
  margin-bottom: 5px

%important_fields
  content: "*"
  position: relative
  font-size: 18px
  color: red

%input_forms
  height: 40px
  width: 100%
  outline: none
  border-radius: 5px
  border: 1px solid #ccc
  padding-left: 15px
  padding-right: 5px
  font-size: 16px
  border-bottom-width: 2px
  transition: all 0.3s ease

.root
  min-width: 700px
  width: 100%
  background: #fff
  padding: 25px 30px
  border-radius: 15px
  box-shadow: 8px 8px 5px 2px #c0c0c0

  .title
    text-align: center
    font-size: 28px
    font-weight: 600
    position: relative
    padding-bottom: $bottomPadTitle

  .sign-up

    .title2
      font-size: 22px
      font-weight: 600
      padding-bottom: $bottomPadTitle

    .personal-info
      display: block
      justify-content: space-between

      .form-group-not-important
        margin: 20px 0 10px 0
        width: 100%

        label
          @extend %form-group-labels

        input, select
           @extend %input_forms

           &::placeholder
            color: #a8acc9

      .form-group
        margin: 20px 0 10px 0
        width: 100%

        label
          @extend %form-group-labels

          &:after
            @extend %important_fields

        input, select
          @extend %input_forms

          &::placeholder
            color: #a8acc9        

      .gender-radio

        .label_gen
          font-size: 18px
          font-weight: 600
          
          &:after
            @extend %important_fields

        #gender
          margin: 14px 0
          display: flex
          width: 15%        
          justify-content: space-between

          label
            margin-right: 5px

          .radio
            width: 15px
            height: 15px

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
        padding: 8px 5px
        justify-content: start
        width: 100%
        
        
        .selected-opt
          padding: 8px 16px
          border-radius: 15px
          background: #e5e5e5
          margin-right: 10px 

      .form-group-check
        margin-top: 20px
        display: flex
        
        input[type=checkbox]
          width: 18px
          height: 18px
          margin: 10px 5px
        label
          padding: 10px 5px
</style>