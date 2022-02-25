<template>
    <div class="side package">
        <cSVG></cSVG>
        <div class="side-container">
            <div class="left top"><a href="/">
            <logoSVG></logoSVG>
            </a></div>
            <div class="middle left">
                <div class="package-info">
                    <div class="package-info__item" v-for="(it, i) in packages_info" :key="i" :class="{'active': it.include.includes(package_num)}">
                        <div class="package-info__item-included">
                            <tickSVG> </tickSVG>
                            </div>
                        <div class="package-info__item-text"> {{it.text}} </div>
                    </div>
                    <div class="change-package">
                        <div class="change-package__txt">Ваш пакет обучения:</div>
                        <div class="change-package__btns">
                            <div class="arrow" @click="setPrev" :class="{'invisible': package_num==1} ">
                                <arlSVG></arlSVG>
                            </div>
                            <div class="current-tarif-name">{{packages[package_num]}}</div>
                            <div class="arrow" @click="setNext" :class="{'invisible': package_num==packagesLen}">
                                <arrSVG></arrSVG>
                            </div>
                        </div>
                    </div>
                </div><a href="/" class="back-to-side-btn"> Вернуться на главную </a>
            </div>
        </div>
    </div>
</template>

<script>

import logoSVG from './svg/logo'
import tickSVG from './svg/tick'
import cSVG from './svg/circle-left'
import arlSVG from './svg/arr-l'
import arrSVG from './svg/arr-r'
export default {
    props: {packages: {type: Object}, package_num: {type: Number}},
    components: { 
        logoSVG,
        cSVG,
        tickSVG,
        arlSVG,
        arrSVG
    },
    data: () => {
        return {
            packages_info: [
                {text: 'Видео-уроки Фрэнка Пьюселика', include: [1, 2, 3]},
                {text: 'Закрытый чат для знакомства общения', include: [1, 2, 3]},
                {text: 'Записи пропущенных онлайн-занятий доступные в течение 7 дней', include: [1, 2, 3]},
                {text: 'Поддержка кураторов', include: [1, 2, 3]},
                {text: 'Еженедельные групповые встречи с тренерами (учениками Фрэнка Пьюселика) для разбора домашних заданий', include: [2, 3]},
                {text: 'Дважды в месяц встречи в прямом эфире с Фрэнком Пьюселиком в формате «Разбор навыка»', include: [3]},
                {text: 'Дважды в месяц встречи в прямом эфире с Фрэнком Пьюселиком в формате «Демонстрация» с ответами на вопросы', include: [3]},
                {text: 'Приоритетная поддержка кураторов', include: [3]},
            ]
        }
    },
    computed: {
        packagesLen(){
            return Object.keys(this.packages).length
        }
    },
    methods: {
        setPrev(){
            let tmp = this.package_num - 1
            if (tmp <= 1) {
                tmp = 1
            }
            this.$emit('package_change', tmp)
        },
        setNext(){
            let tmp = this.package_num + 1
            if (tmp >= this.packagesLen) {
                tmp = this.packagesLen
            }
            this.$emit('package_change', tmp)
        }
    }
}
</script>

<style lang="scss">
.package-info {
    margin-top: 4.27rem;

    @media (max-width: 991px) {
        margin-top:2.27rem
    }

    &__item {
        display: flex;
        align-items: center;
        color: #a3a3a3;
        margin-bottom: 20px;
        transition: color .5s ease;

        &-included {
            fill: #fff;
            max-width: 44px;
            min-width: 44px;
            margin-right: 15px;
            opacity: 0;
            transition: opacity .5s ease;

            @media (max-width: 767px) {
                max-width:25px;
                min-width: 25px;
            }
        }

        &.active {
            color: #fff;
            .package-info__item-included {
                opacity: 1
            }
        }
    }
}

.change-package {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    max-width: calc(100% - 60px);
    margin-left: auto;

    @media (max-width: 991px) {
        max-width:unset;
        margin: 0;
    }

    &__btns {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%
    }

    &__txt {
        color: #abedf0;
        text-transform: uppercase;
        margin-top: 2.77rem;
        margin-bottom: 1.77rem
    }
}

.current-tarif-name {
    background: #abedf0;
    color: #4a4a49;
    font-weight: 700;
    padding: 17px;
    border-radius: 35px;
    width: 100%;
    text-align: center
}

.arrow {
    fill: #fff;
    width: 38px;
    position: relative;
    top: 3px;
    cursor: pointer;
    padding: 5px;
    box-sizing: content-box;
    
    &.invisible {
        opacity: 0;
        pointer-events: none;
    }
}


</style>