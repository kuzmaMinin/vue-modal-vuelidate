<template>
    <div>
        <form @submit.prevent="checkForm">
            <div class="container">
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

                <fieldset>
                    <legend>Адрес</legend>

                    <div class="item">
                        <label for="index" class="title">Индекс</label>
                        <input type="text" v-model.trim="form.index" id="index">
                    </div>

                    <div class="item">
                        <label for="country" class="title">Страна</label>
                        <input type="text" v-model.trim="form.country" id="country">
                    </div>

                    <div class="item">
                        <label for="district" class="title">Область</label>
                        <input type="text" v-model.trim="form.district" id="district">
                    </div>

                    <div class="item">
                        <label for="city" class="title">Город*</label>
                        <input
                            type="text"
                            v-model.trim="form.city"
                            id="city"
                            class=""
                            :class="$v.form.city.$error ? 'is-invalid' : ''"
                        >
                        <p v-if="$v.form.city.$dirty && !$v.form.city.required" class="attention">Обязательное поле!</p>
                    </div>

                    <div class="item">
                        <label for="street" class="title">Улица</label>
                        <input type="text" v-model.trim="form.street" id="street">
                    </div>

                    <div class="item">
                        <label for="building" class="title">Дом</label>
                        <input type="text" v-model.trim="form.building" id="building">
                    </div>

                </fieldset>

                <fieldset>
                    <legend>Паспорт</legend>

                    <div class="item">
                        <label for="documentType" class="title">Тип документа*</label>

                        <select
                            v-model="form.documentTypeItem"
                            id="documentType"
                            class="select-input"
                            :class="$v.form.documentTypeItem.$error ? 'is-invalid' : ''"
                        >
                            <option
                                v-for="(client, index) in documentType"
                                :value="client.value"
                                :key="index"
                            >{{client.label}}
                            </option>
                        </select>
                        <p v-if="$v.form.documentTypeItem.$dirty && !$v.form.documentTypeItem.required" class="attention">Обязательное поле!</p>
                    </div>

                    <div class="item">
                        <label for="series" class="title">Серия</label>
                        <input type="text" v-model.trim="form.series" id="series" >
                    </div>

                    <div class="item">
                        <label for="number" class="title">Номер</label>
                        <input type="text" v-model.trim="form.number" id="number">
                    </div>

                    <div class="item">
                        <label for="issuedBy" class="title">Кем выдан</label>
                        <input type="text" v-model.trim="form.issuedBy" id="issuedBy">
                    </div>

                    <div class="item">
                        <label for="issueDate" class="title">Дата выдачи*</label>
                        <input
                            type="date"
                            v-model="form.issueDate"
                            id="issueDate"
                            placeholder=""
                            class=""
                            :class="$v.form.issueDate.$error ? 'is-invalid' : ''">
                        <p v-if="$v.form.issueDate.$dirty && !$v.form.issueDate.required" class="attention">Обязательное поле!</p>
                    </div>

                </fieldset>
            </div>
                <button type="submit">Отправить</button>
        </form>
        <div v-show="form.showModal" class="allright">
            <h3>Пациент успешно зарегистрирован!</h3>
            <button @click="form.showModal = false">Ок</button>
        </div>
    </div>
</template>

<script>
    import {validationMixin} from 'vuelidate'
    import {required} from 'vuelidate/lib/validators'

    export default {
        mixins: [validationMixin],
        data() {
            return {
                form: {
                    name: '',
                    surname: '',
                    fatherName: '',
                    birthDay: '',
                    phone: '',
                    rusPhone: '',
                    sex: '',
                    clientGroupItems: [],
                    doctor: '',
                    checkSms: false,
                    index: '',
                    country: '',
                    district: '',
                    city: '',
                    street: '',
                    building: '',
                    series: '',
                    number: '',
                    issuedBy: '',
                    issueDate: '',
                    documentTypeItem: '',
                    showModal: false
                },
                clientGroup: [
                    {
                        label: 'VIP',
                        value: 'vip'
                    },
                    {
                        label: 'Проблемные',
                        value: 'problematic'
                    },
                    {
                        label: 'OMC',
                        value: 'omc'
                    }
                ],
                doctors: [
                    {
                        label: 'Иванов',
                        value: 'Ivanov'
                    },
                    {
                        label: 'Захаров',
                        value: 'Zakharov'
                    },
                    {
                        label: 'Чернышева',
                        value: 'Chernysheva'
                    }
                ],
                documentType: [
                    {
                        label: 'Паспорт',
                        value: 'passport'
                    },
                    {
                        label: 'Свидетельство о рождении',
                        value: 'birthCertificate'
                    },
                    {
                        label: 'Водительское удостоверение',
                        value: 'driversLicence'
                    }
                ]

            }
        },
        methods: {
            acceptNumber() {
                var x = this.form.phone.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
                this.form.phone = (!x[2] ? x[1] : '(' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : ''));
                this.form.rusPhone = 7 + this.form.phone
            },
            checkForm() {
                this.$v.form.$touch()
                if (!this.$v.form.$error) {
                    this.form.showModal = true
                }
            },
        },
        validations: {
            form: {
                name: {
                    required,
                },
                surname: {
                    required,
                },
                birthDay: {
                    required
                },
                phone: {
                    required
                },
                clientGroupItems: {
                    required
                },
                city: {
                    required
                },
                issueDate: {
                    required
                },
                documentTypeItem: {
                    required
                }
            }
        }
    }

</script>

<style lang="css">


</style>
