<template>
    <fieldset class="private-information">
        <legend>Личная информация</legend>
        <div class="item">
            <label for="surname" class="title">Фамилия*</label>
            <input
                type="text"
                v-model.trim="form.surname"
                id="surname"
                class=""
                :class="$v.form.surname.$error ? 'is-invalid' : ''"
            >
            <p v-if="$v.form.surname.$dirty && !$v.form.surname.required" class="attention">Обязательное поле!</p>
        </div>


        <div class="item">
            <label for="name" class="title">Имя*</label>
            <input
                type="text"
                v-model.trim="form.name"
                id="name"
                class=""
                :class="$v.form.name.$error ? 'is-invalid' : ''"
            >
            <p v-if="$v.form.name.$dirty && !$v.form.name.required" class="attention">Обязательное поле!</p>
        </div>

        <div class="item">
            <label for="fatherName" class="title">Отчество</label>
            <input type="text" v-model.trim="form.fatherName" id="fatherName" class="">
        </div>

        <div class="item">
            <label for="birthDay" class="title">Дата рождения*</label>
            <input
                type="date"
                v-model="form.birthDay"
                id="birthDay"
                placeholder=""
                class=""
                :class="$v.form.surname.$error ? 'is-invalid' : ''">
            <p v-if="$v.form.birthDay.$dirty && !$v.form.birthDay.required" class="attention">Обязательное поле!</p>
        </div>

        <div class="item" >
            <label for="phone" class="title">Номер телефона*</label>
            <div class="phone-wrapper">
                <span class="pre">+7</span>
                <input
                    v-model="form.phone"
                    type="text"
                    @input="acceptNumber"
                    id="phone"
                    class=""
                    :class="$v.form.surname.$error ? 'is-invalid' : ''">
            </div>
            <p v-if="$v.form.phone.$dirty && !$v.form.phone.required" class="attention">Обязательное поле!</p>
        </div>

        <div class="item">
            <span class="sex-span title">Пол:</span>
            <div class="sex">
                <div class="">
                    <label for="male">Мужской</label>
                    <input type="radio" id="male" value="male" v-model="form.sex">
                </div>
                <div class="">
                    <label for="female">Женский</label>
                    <input type="radio" id="female" value="female" v-model="form.sex">
                </div>
            </div>
        </div>

        <div class="item">
            <label for="clientGroup" class="title">Группа клиентов*</label>
            <select
                v-model="form.clientGroupItems"
                multiple id="clientGroup"
                size="3"
                class="select-input"
                :class="$v.form.clientGroupItems.$error ? 'is-invalid' : ''"
            >
                <option
                    v-for="(client, index) in clientGroup"
                    :value="client.value"
                    :key="index"
                >{{client.label}}
                </option>
            </select>
            <p v-if="$v.form.clientGroupItems.$dirty && !$v.form.clientGroupItems.required" class="attention">Обязательное поле!</p>
        </div>

        <div class="item">
            <label for="doctor" class="title">Лечащий врач</label>
            <select v-model="form.doctor" id="doctor" class="select-input">
                <option
                    v-for="(doctor, index) in doctors"
                    :value="doctor.value"
                    :key="index"
                >{{doctor.label}}
                </option>
            </select>
        </div>

        <div class="annotation">
            <label for="checkSms">Не отправлять СМС </label>
            <input type="checkbox" v-model="form.checkSms" id="checkSms">
        </div>

    </fieldset>
</template>

<script>
    export default {
        name: 'Personal',
        props: {
            msg: String
        }
    }
</script>

<style>

</style>





