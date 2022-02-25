<template>
  <div id="app">
    <div class="app-wrapper">
      <SideLeft :package_num="package_num" :packages="packages" @package_change="handleChange"></SideLeft>
      <SideRight :package_num="package_num" :packages="packages" @package_change="handleChange"
        @open_modal="openModal=true"></SideRight>

      <div v-if="openModal" class="modal-wrapper">
        <div class="modal-inner">
          <div class="modal-container">
            <div class="modal-body">
              <div class="modal-header">Спасибо!</div>
              <div class="modal-text">
                <p>Мы отправили ссылку на указанную почту с доступом к демо-неделе.</p>
                <p><b>Пожалуйста, проверьте почту.</b></p>
              </div>
              <div class="modal-btn-group"><a href="#" class="btn">Отправить заново</a>
              <a @click.prevent="openModal=false" href="#" class="modal-close">Закрыть</a></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SideLeft from './components/sideLeft'
import SideRight from './components/sideRight'

export default {
  name: 'App',
  components: {
    SideLeft,
    SideRight,
  },
  data: ()=>{
    return {
      package_num: 2,
      packages: {
        1: 'Я сам',
        2: 'Хочу результат',
        3: 'Супер результат',
      },
      openModal: true
    }
  },
  methods: {
    handleChange(e){
      this.package_num = +e
    }
  }
}
</script>

<style lang="scss">
.app-wrapper {
    width: 100vw;
    min-height: 100%;
    max-height: 100vh;
    overflow: hidden;
    display: flex;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0
}

@media (max-width: 991px) {
    .app-wrapper {
        display:block;
        overflow-y: scroll;
        max-height: 100%
    }
}

.logo {
    fill: #f4eeea;
    max-width: 267px
}

.back-to-side-btn {
    margin-top: 54px;
    color: #c4c4c4;
    border: 1px solid #c4c4c4;
    font-size: 10px;
    border-radius: 20px;
    padding: 10px 17px;
    transition: all .3s ease
}

.back-to-side-btn:hover {
    background: #0073fa;
    color: #fff;
    border-color: #0073fa
}

.top {
    min-height: 51px;
    display: flex;
    width: 100%;
    align-items: flex-end
}

.top.left {
    justify-content: flex-start;
    margin-top: 20px
}

.top.right {
    justify-content: flex-end;
    font-size: 24px
}

@media (max-width: 991px) {
    .top.right {
        display:none
    }
}

.middle {
    padding-bottom: 60px;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
    z-index: 2
}

.middle.left {
    padding-right: 56px
}

.middle.left .back-to-side-btn {
    margin-left: 60px
}

@media (max-width: 991px) {
    .middle.left {
        padding-right:0
    }

    .middle.left .back-to-side-btn {
        margin-left: 0
    }
}

.middle.right {
    padding-left: 30px
}

@media (max-width: 991px) {
    .middle.right {
        padding-left:0
    }
}

.side {
    min-height: 100%;
    width: 50%;
    max-height: 100vh;
    overflow: hidden auto;
    position: relative
}

@media (max-width: 991px) {
    .side {
        height:auto;
        min-height: auto;
        max-height: unset;
        width: 100%;
        overflow: visible
    }
}

.side.package {
    background-color: #4a4a49;
    color: #fff;
    display: flex;
    justify-content: flex-end
}

@media (max-width: 1190px) {
    .side.package {
        padding-left:30px
    }
}

@media (max-width: 991px) {
    .side.package {
        padding-right:30px;
        justify-content: center
    }
}

@media (max-width: 1190px) {
    .side.form {
        padding-right:30px
    }
}

@media (max-width: 991px) {
    .side.form {
        padding-left:30px;
        justify-content: center
    }
}

.side-container {
    max-width: 590px;
    padding-top: 1.74%;
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column
}

@media (max-width: 991px) {
    .side-container {
        margin:auto
    }
}

.additional-circle-1 {
    width: 385px;
    left: 0;
    bottom: 0;
    transform: translate(-30%,30px);
    z-index: 1
}

@media (max-width: 1386px) {
    .additional-circle-1 {
        transform:translate(-60%,30px)
    }
}

@media (max-width: 991px) {
    .additional-circle-1 {
        width:200px;
        transform: translate(-40%)
    }
}

.additional-circle-2 {
    width: 250px;
    right: 0;
    top: 50%;
    transform: translate(30%);
    z-index: 1
}

.additional-circle-3 {
    width: 105px;
    left: 50%;
    top: 33%;
    transform: translate(-50%);
    z-index: 1
}

.modal-wrapper {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    overflow: hidden;
    background-color: rgba(74,74,73,.48);
    display: flex;
    justify-content: flex-end;
    z-index: 1000
}

.modal-inner {
    width: 50%;
    min-height: 100%;
    display: flex;
    align-items: center
}

@media (max-width: 991px) {
    .modal-inner {
        width:100%
    }
}

.modal-container {
    max-width: 520px;
    width: 100%;
    margin: auto
}

@media (max-width: 991px) {
    .modal-container {
        max-width:unset;
        display: flex;
        justify-content: center
    }
}

.modal-body {
    background-color: #f4eeea;
    border: 1px solid #4a4a49;
    width: 410px;
    padding: 96px 68px 48px;
    text-align: center
}

.modal-body .btn {
    font-size: 18px;
    margin-bottom: 4rem
}

@media (max-width: 575px) {
    .modal-body {
        width:calc(100% - 60px);
        padding: 50px 10px
    }
}

.modal-header {
    font-weight: 700;
    font-size: 2rem;
    margin-bottom: 1em
}

.modal-text {
    margin-bottom: 4.44rem
}

.modal-text p:not(:last-child) {
    margin-bottom: 1em
}

.modal-close {
    font-weight: 300
}

.modal-close:hover {
    text-decoration: underline
}
</style>
