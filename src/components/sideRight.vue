<template>
    <div class="side form">
        <crSVG></crSVG>
        <div class="side-container">
            <div class="right top">
                <div>Просто стать лучше.</div>
            </div>
            <div class="middle right">
                <div class="register-form">
                    <div class="register-form-title">
                        <h1>Попробуйте One Planet Club</h1>
                        <h2>Демо-неделя всего за 20 рублей и далее согласно выбранному тарифу</h2>
                        <p class="register-form-authorize"><a href="/login/index.html">Уже зарегистрированы? Войтите в
                                свой аккаунт</a></p>
                    </div>
                    <div class="register-form-tarifs">
                        <a href="#" v-for="(val, key) in packages" :key="key" class="register-form-tarifs__item"
                            :class="{'active': key == package_num}" @click.prevent="$emit('package_change', key)">
                            {{val}} </a>
                    </div>
                    <form action="" class="register-form-content">
                        <div class="register-form-content__item">
                            <div class="register-form-content__label">Ваше имя и фамилия</div>
                            <div class="register-form-content__input">
                                <input type="text" placeholder="Введите ваши имя и фамилию" v-model="form.name">
                            </div>
                        </div>
                        <div class="register-form-content__item">
                            <div class="register-form-content__label">Ваш email</div>
                            <div class="register-form-content__input">
                                <input type="email" placeholder="Введите ваш email" v-model="form.email">
                            </div>
                        </div>
                        <div class="register-form-content__item">
                            <div class="register-form-content__label">Ваш телефон</div>
                            <div class="register-form-content__input">
                                <masked-input type="tel" autocomplete="off" placeholder="Введите номер телефона" v-model="form.phone"
                                    :guide="true"
                                    :mask="['+', '7', ' ', '(', /[1-9]/, /\d/, /\d/, ')', ' ', /\d/, /\d/, /\d/, '-', /\d/, /\d/, /\d/, /\d/]"
                                >
                                </masked-input>
                            </div>
                        </div>
                        <div class="register-form-content__item promocode-input"><a href="#"
                                @click.prevent="show_promo = !show_promo"
                                class="register-form-content__label">У меня есть промокод
                                <ardSVG></ardSVG>
                                </a>
                            <div class="register-form-content__input" v-if="show_promo"><input type="text"
                                    placeholder="Промокод" v-model="form.promocode">
                                <tickSVG class="input-icon"></tickSVG>
                            </div>
                        </div>
                        <div class="register-form-content__item policy">
                            <el-radio v-model="form.policy" label="1">Нажимая на кнопку "Продолжить",
                                    Вы подтверждаете своё согласие с договором оферты и политикой конфиденциальности</el-radio>
                            </div>
                        <div class="register-form-content__submit">
                            <button
                                class="btn btn-primary btn-rounded btn-shadow btn-shadow-yellow"
                                :disabled="!submitEnabled"    
                                @click="$emit('open_modal')"
                            >Продолжить</button>
                        </div>
                    </form>
                </div><a href="/" class="back-to-side-btn"> Вернуться на главную </a>
            </div>
        </div>
    </div>
</template>

<script>
import crSVG from './svg/circle-right'
import ardSVG from './svg/arr-d'
import TickSVG from './svg/tick.vue'
import MaskedInput from 'vue-text-mask'
import ElRadio from "element-ui/lib/radio";

export default {
    props: {packages: {type: Object}, package_num: {type: Number}},
    components: {
        crSVG,
        ardSVG,
        TickSVG,
        MaskedInput,
        ElRadio
    },
    data: ()=>{
        return {
            show_promo: false,
            header: {
                student: 'студент',
                partner: 'партнер',
            }, 
            form: {
                name: null,
                email: null,
                phone: null,
                promocode: null,
                policy: false
            },
            btns: [
                {name: 'Вход для студентов', tab: 'student'},
                {name: 'Вход для партнеров', tab: 'partner'},
            ]
        }
    },
    computed: {
        nameValid(){
            return this.form.name && this.form.name.length > 2
        },
        emailValid(){
            return /.+@.+\..+/.test(this.form.email)
        },
        submitEnabled(){
            let {phone, policy} = this.form
            return this.nameValid && this.emailValid && phone && policy
        }
    }
}
</script>

<style lang="scss">
@import 'element-ui/packages/theme-chalk/src/radio';


.register-form {
    margin-top: 27px;

    &-title {
        margin: auto;
        max-width: 370px;
        text-align: center;

        h1 {
            font-size: 2.66rem;
            margin: 0 0 30px
        }
        h2 {
            font-size: 1rem;
            font-weight: 400;
            max-width: calc(100% - 30px);
            margin: auto
        }
    }
    &-authorize {
        font-size: 14px;
        color: #c4c4c4;
        text-decoration: underline;
        margin-top: 1rem;
        color: #0073fa
    }
    &-tarifs {
        display: flex;
        justify-content: space-between;
        margin-top: 3.111rem;

        &__item {
            font-size: 14px;
            background-color: #abedf0;
            padding: 14px 5px;
            border-radius: 40px;
            flex: 1 1 160px;
            text-align: center;
            transition: background-color .5s ease;
            display: flex;
            justify-content: center;
            align-items: center;

            @media (max-width: 767px) {
                padding:5px 10px
            }

            &:not(:last-child) {
                margin-right: 1.94rem;

                @media (max-width: 767px) {
                    margin-right:5px
                }
            }

            &.active, &:hover {
                background-color: #fae870
            }
        }
    }

    &-content {
        margin-top: 5rem;

        &__item {
            max-width: calc(100% - 70px);
            margin: 0 auto 29px;

            &.policy {
                text-align: left;
                margin-top: 50px;
                margin-bottom: 40px
            }

            @media (max-width: 575px) {
                max-width:100%;
            }
        }

        &__label {
            margin-bottom: 6px;
            color: #0073fa;
            padding-left: 18px
        }
        &__submit {
            text-align: center
        }
        .promocode-input {
            transition: all .5s ease-out;

            .register-form-content__label {
                color: #2bbd70;
                text-decoration: underline;
                font-weight: 700;
                display: flex;
                align-items: center;
                justify-content: center;

                svg {
                    fill: #2bbd70;
                    position: relative;
                    top: 2px;
                    margin-left: 5px;
                    transition: all .3s ease;

                    &.active {
                        transform: rotate(180deg) translateY(4px)
                    }
                }
            }
            .register-form-content__input {
                position: relative
            }
            input {
                background-color: #2bbd70;
                border: 1px solid transparent;
                color: #fff;
                font-weight: 400;
                text-transform: uppercase;
                font-size: 2rem;
                padding: 0 50px;

                &::placeholder {
                    color: #e4e4e4
                }

                @media (max-width: 575px) {
                    font-size:1.5rem;
                    padding: 0 30px
                }
            }

            .input-icon {
                fill: #fff;
                width: 26px;
                height: 26px;
                position: absolute;
                right: 20px;
                top: 50%;
                transform: translateY(-50%);

                @media (max-width: 575px) {
                    right:10px
                }
            }
        }
    }
}
</style>