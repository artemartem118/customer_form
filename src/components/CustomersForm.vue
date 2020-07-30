<template>
    <form @submit.prevent="onSubmit">
        <div class="form-container">
            <div class="form-title">
                Форма создание клиента
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="lastName"
                        class="form-field__item-label"
                    >
                        Фамилия<span class="star">*</span>:
                    </label>
                    <input
                        v-model.trim="form.lastName"
                        :class="$v.form.lastName.$error ? 'form-field__item-invalid' : ''"
                        class="form-field__item-input"
                        id="lastName"
                        type="text"
                        placeholder="Фамилия клиента"
                    >
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.lastName.$dirty && !$v.form.lastName.required">
                        Это поле обязательно
                    </small>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="firstName"
                        class="form-field__item-label"
                    >
                        Имя<span class="star">*</span>:
                    </label>
                    <input
                        v-model.trim="form.firstName"
                        :class="$v.form.firstName.$error ? 'form-field__item-invalid' : ''"
                        class="form-field__item-input"
                        id="firstName"
                        type="text"
                        placeholder="Имя клиента"
                    >
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.firstName.$dirty && !$v.form.firstName.required">
                        Это поле обязательно
                    </small>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="middleName"
                        class="form-field__item-label"
                    >
                        Отчество:</label>
                    <input
                        v-model.trim="form.middleName"
                        class="form-field__item-input"
                        id="middleName"
                        type="text"
                        placeholder="Отчество клиента"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <div class="form-field__item-label">
                        Дата рождения<span class="star">*</span>:
                    </div>
                    <div class="form-field__item-wrapper">
                        <select
                            v-model="form.birthDate.birthDay"
                            :class="$v.form.birthDate.birthDay.$error ? 'form-field__item-invalid' : ''"
                            class="form-field__item-wrapper__select"
                        >
                            <option
                                v-for="(day, index) in dateData.days"
                                :key="index"
                                :value="day"
                            >
                                {{ day }}
                            </option>
                        </select>
                        <select
                            v-model="form.birthDate.birthMonth"
                            :class="$v.form.birthDate.birthMonth.$error ? 'form-field__item-invalid' : ''"
                            class="form-field__item-wrapper__select"
                        >
                            <option
                                v-for="(month, index) in dateData.months"
                                :key="index"
                                :value="month.value"
                            >
                                {{ month.label }}
                            </option>
                        </select>
                        <select
                            v-model="form.birthDate.birthYear"
                            :class="$v.form.birthDate.birthYear.$error ? 'form-field__item-invalid' : ''"
                            class="form-field__item-wrapper__select"
                        >
                            <option
                                v-for="(year, index) in dateData.years"
                                :key="index"
                                :value="year"
                            >
                                {{ year }}
                            </option>
                        </select>
                    </div>
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.birthDate.$dirty && $v.form.birthDate.$error">
                        Введите корректную дату
                    </small>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="phoneNumber"
                        class="form-field__item-label"
                    >
                        Номер телефона<span class="star">*</span>:</label>
                    <input
                        v-model="form.phoneNumber"
                        :class="$v.form.phoneNumber.$error ? 'form-field__item-invalid' : ''"
                        class="form-field__item-input"
                        id="phoneNumber"
                        type="number"
                        placeholder="Телефон клиента">
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.phoneNumber.$dirty && !$v.form.phoneNumber.startWithSeven">
                        Первая цифра в номере - 7
                    </small>
                    <small v-else-if="$v.form.phoneNumber.$dirty && !$v.form.phoneNumber.lengthNumber">
                        Длина номера - 11 цифр
                    </small>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <div class="form-field__item-label">
                        Пол:
                    </div>
                    <div class="form-field__item-wrapper">
                        <div>
                            <label class="labelCheck" for='male'>
                                <span class="textLabel">Мужчина</span>
                                <input
                                    v-model="form.gender"
                                    id="male"
                                    value="male"
                                    name="gender"
                                    class="checkbox"
                                    type="radio"
                                >
                                <span class="fakeCheck"></span>
                            </label>
                        </div>
                        <div>
                            <label class="labelCheck" for='female'>
                                <span class="textLabel">Женщина</span>
                                <input
                                    v-model="form.gender"
                                    value="female"
                                    id="female"
                                    name="gender"
                                    class="checkbox"
                                    type="radio"
                                >
                                <span class="fakeCheck"></span>
                            </label>
                        </div>
                    </div>
                </div>
            </div>
            <div class="form-field more-height">
                <div class="form-field__item">
                    <label
                        for="customerGroups"
                        class="form-field__item-label"
                    >
                        Группа клиентов<span class="star">*</span>:
                    </label>
                    <div class="form-field__item-wrapper">
                        <select
                            v-model="form.groupCustomers"
                            :class="$v.form.groupCustomers.$error ? 'form-field__item-invalid' : ''"
                            class="form-field__item-wrapper__multiple"
                            id="customerGroups"
                            size="3"
                            multiple
                        >
                            <option
                                v-for="(group, index) in customerGroups"
                                :key="index"
                                :value="group.value"
                            >
                                {{ group.label }}
                            </option>
                        </select>
                    </div>
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.groupCustomers.$dirty && !$v.form.groupCustomers.required">
                        Выберете группу клиентов
                    </small>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="doctor"
                        class="form-field__item-label"
                    >Лечащий врач:</label>
                    <select
                        v-model="form.attendingDoctor"
                        class="form-field__item-wrapper form-field__item-wrapper__select"
                        id="doctor"
                    >
                        <option
                            v-for="(doctor, index) of doctors"
                            :key="index"
                            :value="doctor.value"
                        >
                            {{ doctor.label }}
                        </option>
                    </select>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label class="labelCheck" for="sendMessage">
                        <span class="textLabel">Не отправлять СМС:</span>
                        <input
                            v-model="form.sendMessage"
                            id='sendMessage' name='rememberMe' class="checkbox" type='checkbox'
                        >
                        <span class="fakeCheck"></span>
                    </label>
                </div>
            </div>

            <!--        address     -->

            <div class="form-subtitle">
                Адрес
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="index"
                        class="form-field__item-label"
                    >Индекс:</label>
                    <input
                        v-model="form.index"
                        class="form-field__item-input"
                        id="index"
                        type="number"
                        placeholder="Индекс клиента"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="country"
                        class="form-field__item-label"
                    >Страна:</label>
                    <input
                        v-model="form.country"
                        class="form-field__item-input"
                        id="country"
                        type="text"
                        placeholder="Страна клиента"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="region"
                        class="form-field__item-label"
                    >Область:</label>
                    <input
                        v-model="form.region"
                        class="form-field__item-input"
                        id="region"
                        type="text"
                        placeholder="Область клиента"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="city"
                        class="form-field__item-label"
                    >Город<span class="star">*</span>:</label>
                    <input
                        v-model="form.city"
                        :class="$v.form.city.$error ? 'form-field__item-invalid' : ''"
                        class="form-field__item-input"
                        id="city"
                        type="text"
                        placeholder="Город клиента"
                    >
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.city.$dirty && $v.form.city.$error">
                        Это поле обязательно
                    </small>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="street"
                        class="form-field__item-label"
                    >Улица:</label>
                    <input
                        v-model="form.street"
                        class="form-field__item-input"
                        id="street"
                        type="text"
                        placeholder="Улица клиента"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="house"
                        class="form-field__item-label"
                    >Дом:</label>
                    <input
                        v-model="form.house"
                        class="form-field__item-input"
                        id="house"
                        type="text"
                        placeholder="Дом клиента"
                    >
                </div>
            </div>

            <!--    passport   -->

            <div class="form-subtitle">
                Паспорт
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="documentTypes"
                        class="form-field__item-label"
                    >Тип документа<span class="star">*</span>:</label>
                    <select
                        v-model="form.documentTypes"
                        :class="$v.form.documentTypes.$error ? 'form-field__item-invalid' : ''"
                        class="form-field__item-wrapper form-field__item-wrapper__select"
                        id="documentTypes">
                        <option
                            v-for="(document, index) of documentTypes"
                            :key="index"
                            :value="document.value"
                        >
                            {{ document.label }}
                        </option>
                    </select>
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.documentTypes.$dirty &&$v.form.documentTypes.$error">
                        Выбирите тип документа
                    </small>
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="documentSeries"
                        class="form-field__item-label"
                    >Серия:</label>
                    <input
                        v-model="form.documentSeries"
                        class="form-field__item-input"
                        id="documentSeries"
                        type="number"
                        placeholder="Серия клиента"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="documentNumber"
                        class="form-field__item-label"
                    >Номер:</label>
                    <input
                        v-model="form.documentNumber"
                        class="form-field__item-input"
                        id="documentNumber"
                        type="number"
                        placeholder="Номер клиента"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <label
                        for="documentIssuedBy"
                        class="form-field__item-label"
                    >Кем выдан:</label>
                    <input
                        v-model="form.documentIssuedBy"
                        class="form-field__item-input"
                        id="documentIssuedBy"
                        type="text"
                        placeholder="Кем выдан клиенту"
                    >
                </div>
            </div>
            <div class="form-field">
                <div class="form-field__item">
                    <div class="form-field__item-label">
                        Дата выдачи<span class="star">*</span>:
                    </div>
                    <div class="form-field__item-wrapper">
                        <select
                            v-model="form.documentDateOfIssue.dayOfIssue"
                            :class="$v.form.documentDateOfIssue.dayOfIssue.$error ? 'form-field__item-invalid' : ''"
                            class="form-field__item-wrapper__select"
                        >
                            <option
                                v-for="(day, index) in dateData.days"
                                :key="index"
                                :value="day"
                            >
                                {{ day }}
                            </option>
                        </select>
                        <select
                            v-model="form.documentDateOfIssue.monthOfIssue"
                            :class="$v.form.documentDateOfIssue.monthOfIssue.$error ? 'form-field__item-invalid' : ''"
                            class="form-field__item-wrapper__select"
                        >
                            <option
                                v-for="(month, index) in dateData.months"
                                :key="index"
                                :value="month.value"
                            >
                                {{ month.label }}
                            </option>
                        </select>
                        <select
                            v-model="form.documentDateOfIssue.yearOfIssue"
                            :class="$v.form.documentDateOfIssue.yearOfIssue.$error ? 'form-field__item-invalid' : ''"
                            class="form-field__item-wrapper__select"
                        >
                            <option
                                v-for="(year, index) in dateData.years"
                                :key="index"
                                :value="year"
                            >
                                {{ year }}
                            </option>
                        </select>
                    </div>
                </div>
                <div class="form-field__error">
                    <small v-if="$v.form.documentDateOfIssue.$dirty && $v.form.documentDateOfIssue.$error">
                        Введите корректную дату
                    </small>
                </div>
            </div>
            <div class="form-description">
                <div class="form-description__required">
                    <span class="star">*</span>Поле обязательное для заполнения
                </div>
            </div>
            <div class="form-button">
                <input type="submit" value="Создать">
            </div>
        </div>
    </form>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required } from 'vuelidate/lib/validators'
import dataForValidation from '../mixins/dataForValidation'

export default {
    name: 'CustomersForm',
    mixins: [ validationMixin, dataForValidation ],
    data() {
        return {
            form: {
                lastName: '',
                firstName: '',
                middleName: '',
                birthDate: {
                    birthDay: 'День',
                    birthMonth: 'Месяц',
                    birthYear: 'Год'
                },
                phoneNumber: '7',
                gender: '',
                attendingDoctor: 'Выберите врача',
                groupCustomers: [],
                sendMessage: false,
                index: '',
                country: '',
                region: '',
                city: '',
                street: '',
                house: '',
                documentTypes: 'Выберите тип документа',
                documentSeries: '',
                documentNumber: '',
                documentIssuedBy: '',
                documentDateOfIssue: {
                    dayOfIssue: 'День',
                    monthOfIssue: 'Месяц',
                    yearOfIssue: 'Год'
                }
            }
        }
    },
    validations: {
        form: {
            lastName: { required },
            firstName: { required },
            birthDate: {
                birthDay: {
                    dayValidator( val ) {
                        return val !== 'День'
                    }
                },
                birthMonth: {
                    monthValidator( val ) {
                        return val !== 'Месяц'
                    }
                },
                birthYear: {
                    yearValidator( val ) {
                        return val !== 'Год'
                    }
                }
            },
            groupCustomers: { required },
            city: { required },
            documentTypes: {
                documentValidator( val ) {
                    return val !== 'Выберите тип документа'
                }
            },
            documentDateOfIssue: {
                dayOfIssue: {
                    dayValidator( val ) {
                        return val !== 'День'
                    }
                },
                monthOfIssue: {
                    monthValidator( val ) {
                        return val !== 'Месяц'
                    }
                },
                yearOfIssue: {
                    yearValidator( val ) {
                        return val !== 'Год'
                    }
                }
            },
            phoneNumber: {
                startWithSeven( val ) {
                    return val[0] === '7'
                },
                lengthNumber(val) {
                    return val.length === 11
                }
            }
        }
    },
    methods: {
        onSubmit() {
            this.$v.form.$touch()
            if ( !this.$v.form.$error ) {
                this.$emit('successForm')
            }
        }
    }
}
</script>

<style lang="scss">
@import "../styles/variables";
@import "../styles/mixins";

/* <-- form --> */

.form {
    &-container {
        @include box-shadow-container;

        margin-top: $base * 30;
        margin-bottom: $base * 30;
        padding: $base * 30 $base * 65;
        border-radius: $base * 5;
    }

    &-title {
        padding-bottom: $base * 30;
        font-size: $base * 30;
        text-align: center;
    }

    &-subtitle {
        position: relative;
        text-align: center;
        font-size: $base * 20;
        margin-bottom: $base * 15;
        padding-bottom: $base * 8;

        &:before {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            border-bottom: solid $base * 1 #000;
        }
    }

    &-field {
        display: flex;
        flex-direction: column;
        height: $base * 50;

        &.more-height {
            height: $base * 75;
        }

        &__item {
            display: flex;

            &-label {
                flex-basis: $flex-basis;
                align-self: center;
            }

            &-wrapper {
                display: flex;
                justify-content: space-between;
                flex-basis: $flex-basis;


                &__select {
                    @include select-options;

                    height: $base * 30;
                }

                &__multiple {
                    @include select-options;

                    height: 100%;
                }
            }

            &-input {
                display: inline-block;
                flex-basis: $flex-basis;
                height: $base * 30;
                padding: $base * 2 $base * 5;
                border-width: $base * 1;
                border-radius: $base * 4;
                transition: $delay;

                &::placeholder {
                    font-size: $base * 12;
                }
            }

            &-checkbox {
                display: flex;
                justify-content: flex-end;
                flex-basis: $flex-basis;

                & input {
                    margin: 0;
                    height: $base * 15;
                    width: $base * 15;
                }
            }

            &-invalid {
                border: $base * 1 solid $invalid-color;
            }
        }

        &__error {
            align-self: flex-end;
            color: $invalid-color;
        }
    }

    &-description {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: $base * 50;

        &__required {
            font-size: $base * 13;
            align-self: flex-end;
        }
    }

    &-button {
        text-align: center;

        @include button;

    }
}

/* <-- fake checkbox --> */

.checkbox {
    display: none;

    &:checked + .fakeCheck::before {
        opacity: 1;
    }
}

.labelCheck {
    flex-basis: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.fakeCheck {
    width: $base * 16;
    height: $base * 16;
    position: relative;
    background-color: $black-checkbox-color;

    &::before {
        content: "";
        position: absolute;
        width: $base * 8;
        height: $base * 8;
        background-color: $white-checkbox-color;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        opacity: 0;
        transition: $delay;
    }
}

.textLabel {
    padding-right: $base * 4;
}

/* <-- / fake checkbox --> */

input[type=number],
input[type=text],
select {
    background-color: $white-color;

    &:focus {
        box-shadow: 0 0 $base * 1 $base * 1 #000;
    }
}

.star {
    color: $invalid-color;
    font-size: $base * 15;
}

@media (max-width: $max-width-sm) {
    .form {
        &-container {
            margin-top: $base * 15;
            margin-bottom: $base * 15;
            padding: $base * 15 $base * 30;
        }

        &-title {
            padding-bottom: $base * 15;
            font-size: $base * 20;
        }

        &-field {
            height: $base * 65;

            &.more-height {
                height: $base * 90;
            }

            &__item {
                flex-direction: column;

                &-input {
                    flex-basis: $base * 35;
                }

                &-wrapper__select {
                    flex-basis: $base * 35;
                }

                &-label {
                    align-self: flex-start;
                }
            }
        }
    }
}

/* <-- / form --> */
</style>
