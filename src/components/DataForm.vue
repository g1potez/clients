<script>
import { useVuelidate } from '@vuelidate/core'
import { required, minLength, maxLength, numeric } from '@vuelidate/validators'

export default {
  setup () {
    return { v$: useVuelidate() }
  },
  data () {
    return {
      surname: '',
      name: '',
      birthday: '',
      phone: '',
      client_group: ''
    }
  },
  validations () {
    return {
      surname: {
        required,
        minLength: minLength(2)
      },
      name: {
        required,
        minLength: minLength(2)
      },
      birthday: {
        required
      },
      phone: {
        required,
        minLength: minLength(11),
        maxLength: maxLength(11),
        numeric
      },
      client_group: {
        required
      }
    }
  },
  methods: {
    sendButton() {
      this.v$.$touch();

      if (!this.v$.surname.$error && !this.v$.name.$error && !this.v$.birthday.$error && !this.v$.phone.$error && !this.v$.client_group.$error) {
        this.$emit('formSubmitted');
      }
    }
  }
}
</script>

<template>
    <div class="dataForm blockForm">
          <label for="surname">Фамилия*</label>
          <p v-if="v$.surname.$error" class="field-error">Неккоректное заполнение</p>
          <input type="text" placeholder="Иванов" id="surname" v-model="surname">

          <label for="name">Имя*</label>
          <p v-if="v$.name.$error" class="field-error">Неккоректное заполнение</p>
          <input type="text" placeholder="Иван" id="name" v-model="name">

          <label for="patronymic">Отчество</label>
          <input type="text" placeholder="Иванович" id="patronymic">

          <div class="form-col">
            <figure>
              <label for="birthday">Дата рождения*</label>
              <p v-if="v$.birthday.$error" class="field-error">Выберите дату</p>
              <input type="date" id="birthday" v-model="birthday">
            </figure>
            <figure>
              <label for="phone">Телефон*</label>
              <p v-if="v$.phone.$error" class="field-error">Неккоректное заполнение</p>
              <input type="tel" id="phone" placeholder="79001234567" pattern="[7]{1}[0-9]{3}[0-9]{3}[0-9]{2}[0-9]{2}" maxlength="11" v-model="phone">
            </figure>
          </div>

          <div class="form-col">
            <figure>
              <label for="gender">Пол</label>
              <div id="gender">
                <figure>
                  <input type="radio" id="male" name="gender" value="Мужской" style="margin-right: 10px">
                  <label for="male">Мужской</label>
                </figure>
                <figure>
                  <input type="radio" id="female" name="gender" value="Женский" style="margin-right: 10px">
                  <label for="female">Женский</label>
                </figure>
              </div>
            </figure>
            <figure>
              <label for="client_group">Группа клиентов*</label>
              <p v-if="v$.client_group.$error" class="field-error">Выберите клиента</p>
              <select id="client_group" v-model="client_group">
                <option value="VIP">VIP</option>
                <option value="Проблемные">Проблемные</option>
                <option value="ОМС">ОМС</option>
              </select>
            </figure>
          </div>

          <label for="doctors">Лечащий врач</label>
          <select id="doctors">
            <option autofocus>Выберите врача</option>
            <option value="Иванов">Иванов</option>
            <option value="Захаров">Захаров</option>
            <option value="Чернышева">Чернышева</option>
          </select>

          <button class="next" @click.prevent="sendButton">
            Отправить
          </button>
    </div>
</template>
<style scoped lang="sass">
@import './../assets/variables.sass'

+formBlockStyle
</style>