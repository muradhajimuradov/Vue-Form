<template>
  <div>
    <h1>Регистрационная форма пациента</h1>
    <form @submit.prevent="submit">
      <div class="form-block-title">
        <h2>Личная информация</h2>
      </div>
      <div class="form-block">
        <div class="box">
          <label class="m-10">Имя*:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.firstname.$model" />
            <div class="feedback">
              <span v-if="!$v.firstname.required">Обязательное поле!</span>
              <span
                v-if="!$v.firstname.minLength"
              >Имя должно содержать хотя бы {{$v.firstname.$params.minLength.min}} символ(а/ов)</span>
              <span
                v-if="!$v.firstname.maxLength"
              >Имя не должно превышать {{$v.firstname.$params.maxLength.max}} символ(а/ов)</span>
            </div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Фамилия*:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.lastname.$model" />
            <div class="feedback">
              <span v-if="!$v.lastname.required">Обязательное поле!</span>
              <span
                v-if="!$v.lastname.minLength"
              >Фамилия должна содержать хотя бы {{$v.lastname.$params.minLength.min}} символ</span>
              <span
                v-if="!$v.lastname.maxLength"
              >Имя не должно превышать {{$v.lastname.$params.maxLength.max}} символ</span>
            </div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Отчество:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.patronymic.$model" />
            <div class="feedback"></div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Дата рождения*:</label>
          <div class="m-10">
            <input type="date" v-model.trim="$v.birthdate.$model" />
            <div class="feedback">
              <span v-if="!$v.birthdate.required">Обязательное поле!</span>
            </div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Номер телефона*:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.phone.$model" />
            <div class="feedback">
              <span v-if="!$v.phone.required">Обязательное поле!</span>
              <span
                v-if="!$v.phone.minLength"
              >Телефон должен содержать {{$v.phone.$params.minLength.min}} символов</span>
              <span
                v-if="!$v.phone.maxLength"
              >Телефон не должен превышать {{$v.phone.$params.maxLength.max}} символов</span>
              <span v-if="!$v.phone.phoneValid">Первая цифра должна быть 7</span>
            </div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Пол:</label>
          <div class="m-10">
            <select v-model.trim="$v.gender.$model">
              <option value="Male">Мужчина</option>
              <option value="Female">Женщина</option>
            </select>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Группа клиентов*:</label>
          <div class="m-10">
            <select v-model.trim="$v.typeOfClient.$model">
              <option value="VIP">VIP</option>
              <option value="With problems">Проблемные</option>
              <option value="CHI">ОМС</option>
            </select>
            <div class="feedback">
              <span v-if="!$v.typeOfClient.required">Обязательное поле!</span>
            </div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Лечащий врач:</label>
          <div class="m-10">
            <select v-model.trim="$v.doctor.$model">
              <option value="Ivanov">Иванов</option>
              <option value="Zaharov">Захаров</option>
              <option value="Chernysheva">Чернышева</option>
            </select>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Не отправлять смс:</label>
          <div class="m-10">
            <input type="checkbox" v-model.trim="$v.doNotSendSms.$model" />
          </div>
        </div>
      </div>
      <div class="form-block-title">
        <h2>Адрес</h2>
      </div>
      <div class="form-block">
        <div class="box">
          <label class="m-10">Индекс:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.index.$model" />
          </div>
        </div>
        <div class="box">
          <label class="m-10">Страна:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.country.$model" />
          </div>
        </div>
        <div class="box">
          <label class="m-10">Область:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.region.$model" />
          </div>
        </div>
        <div class="box">
          <label class="m-10">Город*:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.city.$model" />
            <div class="feedback">
              <span v-if="!$v.city.required">Обязательное поле</span>
              <span
                v-if="!$v.city.minLength"
              >Название города должно содержать хотя бы {{$v.city.$params.minLength.min}} символ(а/ов)</span>
              <span
                v-if="!$v.city.maxLength"
              >Название города не должно превышать {{$v.city.$params.maxLength.max}} символ(а/ов)</span>
            </div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Улица:</label>
          <div class="m-10">
            <input
              type="text"
              v-model.trim="$v.street.$model"
              :class="{'is-invalid':$v.street.$error, 'is-valid':!$v.street.$invalid}"
            />
          </div>
        </div>
        <div class="box">
          <label class="m-10">Дом:</label>
          <div class="m-10">
            <input
              type="text"
              v-model.trim="$v.house.$model"
              :class="{'is-invalid':$v.house.$error, 'is-valid':!$v.house.$invalid}"
            />
          </div>
        </div>
      </div>
      <div class="form-block-title">
        <h2>Паспорт</h2>
      </div>
      <div class="form-block">
        <div class="box">
          <label class="m-10">Тип документа*:</label>
          <div class="m-10">
            <select v-model.trim="$v.documentType.$model">
              <option value="passport">Паспорт</option>
              <option value="birthCertificate">Свидетельство о рождении</option>
              <option value="driverLicence">Вод. удостоверение</option>
            </select>
            <div class="feedback">
              <span v-if="!$v.documentType.required">Обязательное поле!</span>
            </div>
          </div>
        </div>
        <div class="box">
          <label class="m-10">Серия:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.documentSeries.$model" />
          </div>
        </div>
        <div class="box">
          <label class="m-10">Номер:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.documentNumber.$model" />
          </div>
        </div>
        <div class="box">
          <label class="m-10">Кем выдан:</label>
          <div class="m-10">
            <input type="text" v-model.trim="$v.documentSource.$model" />
          </div>
        </div>
        <div class="box">
          <label class="m-10">Дата выдачи*:</label>
          <div class="m-10">
            <input type="date" v-model.trim="$v.documentDate.$model" />
            <div class="feedback">
              <span v-if="!$v.documentDate.required">Обязательное поле!</span>
            </div>
          </div>
          <div class="feedback">
            
          </div>
        </div>
      </div>
      <button class="button" type="submit" :disabled="submitStatus === 'PENDING'">Отправить форму!</button>
      <p class="typo__p" v-if="submitStatus === 'OK'">Спасибо за регистрацию</p>
      <p class="typo__p" v-if="submitStatus === 'ERROR'">Пожалуйста заполните форму правильно</p>
      <p class="typo__p" v-if="submitStatus === 'PENDING'">Отправляется...</p>
      <!-- <pre>{{$data}}</pre> -->
    </form>
  </div>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";
// const currentDate = moment(new Date()).startOf('day');
// const minDate = window.vuelidate.withParams({minDate: currentDate.format('DD.MM.YYYY')}, value => moment(value, 'DD.MM.YYYY', true).isSameOrAfter(currentDate));

const isFirstSeven = (value) => value.startsWith("7");
export default {
  name: "Form",
  data() {
    return {
      firstname: "",
      lastname: "",
      patronymic: "",
      birthdate: "",
      phone: "",
      gender: "",
      typeOfClient: "",
      doctor: "",
      doNotSendSms: false,
      index: "",
      country: "",
      region: "",
      city: "",
      street: "",
      house: "",
      documentType: "",
      documentSeries: "",
      documentNumber: "",
      documentSource: "",
      documentDate: "",
      submitStatus: null,
    };
  },
  methods: {
    submit() {
      console.log("submit!");
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        // do your submit logic here
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
        }, 500);
      }
    },
  },
  validations: {
    firstname: {
      required,
      minLength: minLength(1),
      maxLength: maxLength(30),
    },
    lastname: {
      required,
      minLength: minLength(1),
      maxLength: maxLength(30),
    },
    patronymic: {
    },
    birthdate: {
      required,
    },
    phone: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
      phoneValid: isFirstSeven,
    },
    gender: {},
    typeOfClient: {
      required,
    },
    doctor: {},
    doNotSendSms: {},
    index: {},
    country: {},
    region: {},
    city: {
      required,
      minLength: minLength(1),
      maxLength: maxLength(30),
    },
    street: {},
    house: {},
    documentType: {
      required,
    },
    documentSeries: {},
    documentNumber: {},
    documentSource: {},
    documentDate: {
      required,
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
.feedback
  font-size: 70%
  color: red

.form-block-title
  background: white
  margin: auto

.form-block-title h2
  font-size: 90%

.form-block
  border: 1px solid rgba(0,0,0,0.1)
  border-radius: 10px
  display: flex
  flex-wrap: wrap
  margin: 10px

.box
  padding: 15px
  flex-grow: 1
  flex-basis: 25%
  display: inline-block
  white-space: nowrap

.box > div > input
  border-radius: 5px
  border: 1px solid rgba(0,0,0,0.1)
  background: wheat

.box > div > select
  border-radius: 5px
  border: 1px solid rgba(0,0,0,0.1)
  background: wheat

.m-10
  margin: 10

span 
  display: block


</style>
