<script>
import { useVuelidate } from '@vuelidate/core'
import { required } from '@vuelidate/validators'
export default {
    setup() {
        return { v$: useVuelidate() }
    },
    data() {
        return {
            doc_type: '',
            got_passport: ''
        }
    },
    validations() {
        return {
            doc_type: {
                required
            },
            got_passport: {
                required
            }
        }
    },
    methods: {
        sendButton() {
            this.v$.$touch();

            if (!this.v$.doc_type.$error && !this.v$.got_passport.$error) {
                this.$emit('formSubmitted');
            }
        }
    }
}
</script>
<template>
    <div class="passportForm blockForm">
        <label for="doc_type">Тип документа*</label>
        <p v-if="v$.doc_type.$error" class="field-error">Выберите документ</p>
        <select id="doc_type" v-model="doc_type">
            <option value="Паспорт">Паспорт</option>
            <option value=">Свидетельство о рождении">Свидетельство о рождении</option>
            <option value=" Вод. удостоверение"> Вод. удостоверение</option>
        </select>

        <div class="form-col">
            <figure>
                <label for="serial">Серия</label>
                <input type="number" placeholder="5111" id="serial" maxlength="4" >
            </figure>
            <figure>
                <label for="number">Номер</label>
                <input type="number" placeholder="123456" id="number" maxlength="6">
            </figure>
        </div>

        <label for="who">Кем выдан</label>
        <input type="text" placeholder="Кем выдан" id="who">

        <label for="got_passport">Дата получения*</label>
        <p v-if="v$.got_passport.$error" class="field-error">Выберите дату</p>
        <input type="date" id="got_passport" v-model="got_passport">

        <button type="submit" class="sendButton" @click.prevent="sendButton">Отправить</button>
    </div>
</template>

<style scoped lang="sass">
@import './../assets/variables.sass'

+formBlockStyle
.passportForm
    display: none
    transform: translateX(500px)
    select
        margin-bottom: 20px
</style>