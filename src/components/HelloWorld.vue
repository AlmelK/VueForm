<template>
  <div class="root">
    <form class="sign-up">
      <div class="personal-info">
        <h2>Личные данные</h2>

        <div class="form-group">
          <label for="surName">Фамилия*</label>
          <input type="text" id="surName" v-model="surname" />
        </div>
        <div class="form-group">
          <label for="name">Имя*</label>
          <input type="text" id="name" v-model="clientName" />
        </div>
        <div class="form-group">
          <label for="third_name">Отчество</label>
          <input type="text" id="third_name" v-model="thirdName" />
        </div>
        <div class="form-group">
          <label for="birth_day">Дата рождения*</label>
          <input type="date" id="birth_day" v-model="birthday" />
        </div>
        <div class="form-group">
          <label for="phone">Номер телефона*</label>
          <input type="tel" id="phone" v-model="phoneNumber" />
        </div>
        <div class="form-group">
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

        <div class="form-group">
          <input type="checkbox" id="sms" v-model="notSendSMS">
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
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
