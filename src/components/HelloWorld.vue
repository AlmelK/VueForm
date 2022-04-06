<template>
  <div class="root">
    <div class="title">Регистрация</div>
    <form class="sign-up">
      <div class="title2">Личные данные</div>
      <div class="personal-info">

        <div class="form-group">
          <label for="surName">Фамилия*</label>
          <input type="text" id="surName" v-model="surname" placeholder="Введите вашу фамилию"/>
        </div>
        <div class="form-group">
          <label for="name">Имя*</label>
          <input type="text" id="name" v-model="clientName" placeholder="Введите ваше имя"/>
        </div>
        <div class="form-group">
          <label for="third_name">Отчество</label>
          <input type="text" id="third_name" v-model="thirdName" placeholder="Введите ваше отчество"/>
        </div>
        <div class="form-group">
          <label for="birth_day">Дата рождения*</label>
          <input type="date" id="birth_day" v-model="birthday" placeholder="Введите вашу дату рождения"/>
        </div>
        <div class="form-group">
          <label for="phone">Номер телефона*</label>
          <input type="tel" id="phone" v-model="phoneNumber" placeholder="Введите ваш номер телефона"/>
        </div>
        <div class="form-group-radio">
          <label for="chooseGender">Пол*</label>
          <div id="chooseGender" v-for="(gend, index) in genders" :key="index">
            <input type="radio" :value="gend.value" v-model="gender" />
            {{ gend.gen }}
          </div>
        </div>

        <div class="form-group">
          <label for="clientGroup">Группа клиентов*</label>
          <select id="clientGroup" v-model="selectedGroups" multiple>
            <option
              v-for="(g, index) in clientsGroup"
              :value="g.value"
              :key="index"
            >
              {{ g.group }}
            </option>
          </select>
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
      genders: [
        {
          gen: "М",
          value: "male",
        },
        {
          gen: "Ж",
          value: "female",
        },
      ],
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
      selectedGroups: ["OMS"],
      doctor: "",
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
      notSendSMS: false,
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

      .form-group
        margin: 20px 0 10px 0
        width: 100%

        label
          @extend %form-group-labels

        input 
          height: 45px
          width: 100%
          outline: none
          border-radius: 5px
          border: 1px solid #ccc
          padding-left: 15px
          font-size: 16px
          border-bottom-width: 2px
          transition: all 0.3s ease

          &:focus
            border-color: #696969
      
      .form-group-radio
        margin: 20px 0 10px 0
        width: 100%

        label
          @extend %form-group-labels

        #chooseGender
          width: 80%
          display: inline-block
          justify-content: space-around
          

      
</style>
