<template>
  <div class="container">
    <form class="regForm" @submit.prevent="registerUser" novalidate>

      
       
      <div v-show="step === 1" class="step">
      <p class="formTitle">Персональные данные</p>
      <div class="form-group">
        <label for="lastNameInput">Фамилия</label>
        <input
          v-model="$v.lastNameInput.$model"
          :class="{'is-invalid': $v.lastNameInput.$error}"
          type="text"
          class="form-control"
          id="lastNameInput"
          placeholder="Иванов"          
        />
        <div v-if="!$v.lastNameInput.required" class="invalid-feedback">Поле обязательно для заполнения</div>
        <div v-if="!$v.lastNameInput.alpha" class="invalid-feedback">Поле не должно содержать цифр или других символов</div>

        <label for="firstNameInput">Имя</label>
        <input
          type="text"
          v-model="$v.firstNameInput.$model"
          :class="{'is-invalid': $v.firstNameInput.$error}"
          class="form-control"
          id="firstNameInput"
          placeholder="Иван"
          name="firstNameInput"
        />
        <div v-if="!$v.firstNameInput.required" class="invalid-feedback">Поле обязательно для заполнения</div>
        <div v-if="!$v.firstNameInput.alpha" class="invalid-feedback">Поле не должно содержать цифр или других символов</div>

      </div>
      
      <div class="form-group">
        <label for="secondNameInput">Отчество</label>
        <input
          v-model="$v.secondNameInput.$model"
          :class="{'is-invalid': $v.secondNameInput.$error}"
          type="text"
          class="form-control"
          id="secondNameInput"
          placeholder="Иванович"
          name="secondNameInput"
        />
        <div v-if="!$v.secondNameInput.alpha" class="invalid-feedback">Поле не должно содержать цифр или других символов</div>
      </div>
      
      <div class="form-group">
        <label for="birthDateInput">Дата рождения</label>
        <input
          v-model="$v.birthDateInput.$model"
          :class="{'is-invalid': $v.birthDateInput.$error}"
          type="date"
          class="form-control"
          id="birthDateInput"
          placeholder="01.01.1990"
          name="birthDateInput"
        />
        <div v-if="!$v.birthDateInput.required" class="invalid-feedback">Поле обязательно для заполнения</div>
      </div>
      
      <div class="form-group">
        <label for="phoneNumber">Номер телефона</label>
        <input
          v-model="$v.phoneNumber.$model"
          :class="{'is-invalid': $v.phoneNumber.$error}"
          type="tel"
          class="form-control"
          id="phoneNumber"
          placeholder="79991234567"
          name="phoneNumber"
        />
        <div v-if="!$v.phoneNumber.required" class="invalid-feedback">Поле обязательно для заполнения</div>
        <div v-if="!$v.phoneNumber.phone" class="invalid-feedback">Номер телефона состоит из цифр, начинается с "7", пример: 79991234567</div>
      </div>
      
      <div class="form-group">
        <label for="sexInput">Пол</label>
        <select id="sexInput" class="selector">
          <option class="selector-item">Мужской</option>
          <option class="selector-item">Женский</option>
        </select>
      </div>
      
      <div class="form-group">
        <label for="clientGroupInput">Группа клиентов:</label>
        <select
          v-model="$v.clientGroupInput.$model"
          :class="{'is-invalid': $v.clientGroupInput.$error}"
          name="clientGroupInput[]"
          multiple
          size="3"
          class="selector"
          id="clientGroupInput"
        >
          <option value="VIP" class="selector-item">VIP</option>
          <option value="Проблемные" class="selector-item">Проблемные</option>
          <option value="ОМС" class="selector-item">ОМС</option>
        </select>
        <div v-if="!$v.clientGroupInput.required" class="invalid-feedback">Необходимо выбрать минимум один параметр</div>
      </div>
      
      <div class="form-group">
        <label for="doctorInput">Лечащий врач</label>
        <select id="doctorInput" class="selector">
          <option class="selector-item">Иванов</option>
          <option class="selector-item">Захаров</option>
          <option class="selector-item">Чернышева</option>
        </select>
      </div>
      
      
      <div class="form-group">
        <label for="smsDeniedInput">Не отправлять СМС</label>
        <input
          type="checkbox"
          class="form-control"
          id="smsDeniedInput"
          name="smsDeniedInput"
        />
      </div>
      <button class="btn"
            :disabled="disabledBtn1"
            @click="nextStep" type="button">Следующий шаг</button>
      </div>


      <transition name="slide-fade">
      <div v-show="step === 2" class="step">
      <p class="formTitle">Адрес</p>
      <div class="form-group">
        <label for="indexInput">Индекс</label>
        <input
          v-model="$v.indexInput.$model"
          :class="{'is-invalid': $v.indexInput.$error}"
          type="text"
          class="form-control"
          id="indexInput"
          placeholder="443056"
          name="indexInput"
        />
        <div v-if="!$v.indexInput.numeric" class="invalid-feedback">Индекс может состоять только из цифр</div>
        <div v-if="!$v.indexInput.minLength" class="invalid-feedback">Длина индекса составляет 6 цифр</div>
        <div v-if="!$v.indexInput.maxLength" class="invalid-feedback">Длина индекса составляет 6  цифр</div>

        <label for="countryInput">Страна</label>
        <input
          v-model="$v.countryInput.$model"
          :class="{'is-invalid': $v.countryInput.$error}"
          type="text"
          class="form-control"
          id="countryInput"
          placeholder="Россия"
          name="countryInput"
        />
        <div v-if="!$v.countryInput.alpha" class="invalid-feedback">В поле не должно быть цифр или других символов</div>
      </div>
      
      <div class="form-group">
        <label for="regionInput">Область</label>
        <input
          v-model="$v.regionInput.$model"
          :class="{'is-invalid': $v.regionInput.$error}"
          type="text"
          class="form-control"
          id="regionInput"
          placeholder="Самарская область"
          name="regionInput"
        />
        <div v-if="!$v.regionInput.alpha" class="invalid-feedback">В поле не должно быть цифр или других символов</div>
      </div>
      
      <div class="form-group">
        <label for="cityInput">Город</label>
        <input
          v-model="$v.cityInput.$model"
          :class="{'is-invalid': $v.cityInput.$error}"
          type="text"
          class="form-control"
          id="cityInput"
          placeholder="Самара"
          name="cityInput"
        />
        <div v-if="!$v.cityInput.required" class="invalid-feedback">Поле обязательно для заполнения</div>
        <div v-if="!$v.cityInput.alpha" class="invalid-feedback">В поле не должно быть цифр или других символов</div>
      </div>
      
      <div class="form-group">
        <label for="streetInput">Улица</label>
        <input
          v-model="$v.streetInput.$model"
          :class="{'is-invalid': $v.streetInput.$error}"
          type="text"
          class="form-control"
          id="streetInput"
          placeholder="Ленина"
          name="streetInput"
        />
        <div v-if="!$v.streetInput.alphaNum" class="invalid-feedback">В поле допустимо использовать только цифры и буквы</div>
        
        <label for="houseInput">Дом</label>
        <input
          v-model="$v.houseInput.$model"
          :class="{'is-invalid': $v.houseInput.$error}"
          type="text"
          class="form-control"
          id="houseInput"
          placeholder="1"
          name="houseInput"
        />
        <div v-if="!$v.houseInput.alphaNum" class="invalid-feedback">В поле допустимо использовать только цифры и буквы</div>
      </div>
      <button class="btn btn-prev" @click="backStep" type="button">Предыдущий шаг</button>
      <button 
          :disabled="disabledBtn2" class="btn"
          @click="nextStep" type="button">Следующий шаг</button>
      </div>
      </transition>


      <transition name="slide-fade">
      <div v-show="step === 3" class="step">
      <p class="formTitle">Паспорт</p>
      <div class="form-group">
        <label for="docTypeInput">Тип документа</label>
        <select 
          class="selector"
          v-model="$v.docTypeInput.$model"
          :class="{'is-invalid': $v.docNumberInput.$error}"
          id="docTypeInput">
          <option class="selector-item">Паспорт</option>
          <option class="selector-item">Свидетельство о рождении</option>
          <option class="selector-item">Вод. удостоверение</option>
        </select>
        <div v-if="!$v.docTypeInput.required" class="invalid-feedback">Поле обязательно для заполнения</div>
      </div>
      
      <div class="form-group">
        <label for="serialNumberInput">Серия</label>
        <input
          v-model="$v.serialNumberInput.$model"
          :class="{'is-invalid': $v.serialNumberInput.$error}"
          type="text"
          class="form-control"
          id="serialNumberInput"
          placeholder="3601"
          name="serialNumberInput"
        />
        <div v-if="!$v.serialNumberInput.numeric" class="invalid-feedback">Серия документа состоит из 4-х цифр</div>
        <div v-if="!$v.serialNumberInput.minLength" class="invalid-feedback">Серия документа состоит из 4-х цифр</div>
        <div v-if="!$v.serialNumberInput.maxLength" class="invalid-feedback">Серия документа состоит из 4-х цифр</div>

        <label for="docNumberInput">Номер</label>
        <input
          v-model="$v.docNumberInput.$model"
          :class="{'is-invalid': $v.docNumberInput.$error}"
          type="text"
          class="form-control"
          id="docNumberInput"
          placeholder="123456"
          name="docNumberInput"
        />
        <div v-if="!$v.docNumberInput.numeric" class="invalid-feedback">Номер документа состоит из 6 цифр</div>
        <div v-if="!$v.docNumberInput.minLength" class="invalid-feedback">Номер документа состоит из 6 цифр</div>
        <div v-if="!$v.docNumberInput.maxLength" class="invalid-feedback">Номер документа состоит из 6 цифр</div>

      </div>
      
      <div class="form-group">
        <label for="docReleaserInput">Кем выдан</label>
        <input
          v-model="$v.docReleaserInput.$model"
          :class="{'is-invalid': $v.docReleaserInput.$error}"
          type="text"
          class="form-control"
          id="docReleaserInput"
          placeholder="МФЦ по Октябрьскому району"
          name="docReleaserInput"
        />
        <div v-if="!$v.docReleaserInput.alpha" class="invalid-feedback">В поле не должно быть цифр или других символов</div>
      </div>
      
      <div class="form-group">
        <label for="releaseDateInput">Дата выдачи</label>
        <input
          v-model="$v.releaseDateInput.$model"
          :class="{'is-invalid': $v.releaseDateInput.$error}"
          type="date"
          class="form-control"
          id="releaseDateInput"
          placeholder="01.01.1990"
          name="releaseDateInput"
        />
        <div v-if="!$v.releaseDateInput.required" class="invalid-feedback">Поле обязательно для заполнения</div>
      </div>
      <button class="btn btn-prev" @click="backStep" type="button">Предыдущий шаг</button>
      <button class="btn"
          :disabled="disabledBtn3"
          type="submit">Зарегистрироваться</button>
      </div>
      </transition>
    </form>
    
  </div>
</template>

<script>
import { required, helpers, numeric, maxLength, minLength } from 'vuelidate/lib/validators'

const alpha = helpers.regex('alpha', /^[a-zA-Zа-яёА-ЯЁ]*$/);
const phone = helpers.regex('phone', /^((7)+([0-9]){10})$/);
const alphaNum = helpers.regex('alphaNum', /^[a-zA-Zа-яёА-ЯЁ0-9]*$/);

export default {
  data () {
    return {
      step: 1,
      lastNameInput:'',
      firstNameInput:'',
      secondNameInput:'',
      birthDateInput:'',
      phoneNumber:'',
      sexInput:'',
      clientGroupInput:'',
      doctorInput:'',
      smsDeniedInput:'',
      indexInput:'',
      countryInput:'',
      regionInput:'',
      cityInput:'',
      streetInput:'',
      houseInput:'',
      docTypeInput:'',
      serialNumberInput:'',
      docNumberInput:'',
      docReleaserInput:'',
      releaseDateInput:''
    }    
  },
  computed: {
      disabledBtn1() {
        return this.$v.lastNameInput.$invalid ||
               this.$v.firstNameInput.$invalid ||
               this.$v.secondNameInput.$invalid ||
               this.$v.birthDateInput.$invalid ||
               this.$v.phoneNumber.$invalid 
              // || this.$v.clientGroupInput.$invalid
      },
      disabledBtn2 (){
        return this.$v.indexInput.$invalid ||
               this.$v.countryInput.$invalid ||
               this.$v.regionInput.$invalid ||
               this.$v.cityInput.$invalid ||
               this.$v.streetInput.$invalid ||
               this.$v.houseInput.$invalid
      },
      disabledBtn3 (){
        return this.$v.docTypeInput.$invalid ||
               this.$v.serialNumberInput.$invalid ||
               this.$v.docNumberInput.$invalid ||
               this.$v.docReleaserInput.$invalid ||
               this.$v.releaseDateInput.$invalid
      }
  },
  methods: {
      nextStep() {
        this.step++;
      },
      backStep() {
        this.step--;
      },
      registerUser() {
        alert('Новый клиент успешно создан');
        this.step = 1;
        this.lastNameInput='';
        this.firstNameInput = '';
        this.secondNameInput = '';
        this.birthDateInput = '';
        this.phoneNumber = '';
        this.sexInput = '';
        this.clienGroupInput = '';
        this.doctorInput = '';
        this.smsDeniedInput = '';
        this.indexInput = '';
        this.countryInput = '';
        this.regionInput = '';
        this.cityInput = '';
        this.streetInput = '';
        this.houseInput = '';
        this.docTypeInput = '';
        this.serialNumberInput = '';
        this.docNumberInput = '';
        this.docReleaserInput = '';
        this.releaseDateInput = '';
        this.$v.$reset();
      }
  },
  validations: {
      lastNameInput: {
        required,
        alpha,        
      },
      firstNameInput:{
        required,
        alpha,
      },
      birthDateInput:{
        required,
      },
      phoneNumber:{
        required,
        phone,
      },
      clientGroupInput:{
        required,
      },
      cityInput:{
        required,
        alpha,
      },
      docTypeInput:{
        required
      },
      releaseDateInput:{
        required
      },
      secondNameInput: {
        alpha
      },
      indexInput: {
        numeric,
        maxLength: maxLength(6),
        minLength: minLength(6),
      },
      countryInput: {
        alpha
      },
      regionInput: {
        alpha
      },
      streetInput: {
        alphaNum
      },
      houseInput: {
        alphaNum
      },
      serialNumberInput:{
        numeric,
        minLength: minLength(4),
        maxLength: maxLength(4),
      },
      docNumberInput:{
        numeric,
        minLength: minLength(6),
        maxLength: maxLength(6),
      },
      docReleaserInput: {
        alpha,
      },
  }  
};
</script>

<style>
*, *:before, *:after {
    box-sizing: border-box;
}

.container {
    max-width: 1140px;
    margin: auto;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    color: #444;
    background: rgb(21, 21, 21);
}


.regForm{
    position: relative;
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;
    width: 90%;
    border-radius: 10px;
    margin: 100px auto;
    background: #424242;
    box-shadow: 10px 10px 15px 15px rgba(0, 0, 0, 0.7);
    padding: 40px;
    color: rgb(256, 256, 256, 0.7);
}

Input {
  border-radius: 10px;
  color: white;
  background-color: #343434;
  margin-left: 1%;
}

.slide-fade-enter-active {
  transition: all .3s ease;
}

.form-group{
  display: flex;
  margin-top: 5%;
}

.slide-fade-enter {
  transform: translateX(10px);
  opacity: 0;
}

.is-invalid {
  border-color: red;
}

.invalid-feedback{
  color: red;
  font-size: 0.7rem;
  font-style: italic;
}

.btn {
  display: flex;
  cursor: pointer;
  border-radius: 3px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #BB86Fc;
  box-shadow: 5px 5px 5px black;
  transition: all .2s ease;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -ms-border-radius: 3px;
  -o-border-radius: 3px;
  user-select: none;
  color: white;
  margin-top: 10px;
}

.btn:hover, .btn:focus {
  background-color: #03DAC6;
}

@media (max-width:1200px) {
    .container {
        max-width: 960px;
    }
    
}
@media (max-width:992px){
    .container {
        max-width: 740px;
    }
    .form-group{
        flex-direction: column;
        
    }
    
}
@media (max-width: 768px) {
    .container {
        max-width: 540px;
    }
    
    
}
@media (max-width: 578px) {
    .container {
        max-width: 90%;
    }
    .btn {
        width: 100%;
    }
    
    
}

.selector {
  margin-left: 5px;
  background-color: #343434;
  color:white;
  border-radius: 10px;
  overflow-y: auto;
}


</style>
