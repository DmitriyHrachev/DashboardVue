
<template>

<div style="height: 100%">
<Header v-on:openModal="openModal" />

    <div class="wrapper">
        <div class="col-4">
            <div class="inner-col">				
                <div class="panel panel--no-pd">
                    <Clock />
                </div>
                <SchoolResult v-bind:groups="groups" />
            </div>
        </div>
        <div class="col-3">
            <div class="inner-col">
            <SchoolResultDetails v-bind:groups="groups" />
            </div>
        </div>
        <div class="col-5">
            <div class="inner-col">
                <AmountStudies v-bind:groups="groups" />
                <InfoCard v-bind:cards="cards" />
            </div>
        </div>
    </div>
    <Modal v-show="showModal" v-on:closeModal="closeModal" v-on:cardValues="getCardValues" v-on:submitForm="getModalData" />
</div>
</template>

<script>
import AmountStudies from './components/AmountStudies.vue'
import Clock from './components/Clock.vue'
import Header from './components/Header.vue'
import InfoCard from './components/InfoCard/InfoCard.vue'
import Modal from './components/Modal/Modal.vue'
import SchoolResult from './components/SchoolResult.vue'
import SchoolResultDetails from './components/SchoolResultDetails.vue'
export default {
  components: { AmountStudies, InfoCard, Clock, SchoolResult, SchoolResultDetails, Header, Modal },  
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      showModal: false,
      groups: [],
      cards: {
          infoCard: {
				  name: "מספר אירועים פתוחים",
				  value: 3
			  },
			  infoCard2: {
				  name: "חניכים בתהליך קליטה",
				  value: 18
			  },
			  infoCard3: {
				  name: "מספר תקלות פתוחות",
				  value: 12
			  }
      },
      openModal: () => {
        this.showModal = true;
      },
      closeModal: () => {
        this.showModal = false;
      },
      getModalData: (groups) => {
          this.groups = [...groups];
          this.closeModal();
      },
      getCardValues: (cards) => {
          this.cards = cards;
      }
    }
  }
  
}
</script>

<style lang="scss">
.required {
    border: 1px solid red!important;
}
.form__disabled {
    border: 1px solid red!important;
}
@font-face{
    font-family: 'Heebo';
    src: url('./fonts/Heebo-Medium.woff2') format('woff2'), url('./fonts/Heebo-Medium.woff') format('woff');
    font-weight: 500;
    font-style: normal;
}

@font-face{
    font-family: 'Heebo';
    src: url('./fonts/Heebo-Regular.woff2') format('woff2'), url('./fonts/Heebo-Regular.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}

@font-face{
    font-family: 'Heebo';
    src: url('./fonts/Heebo-Bold.woff2') format('woff2'), url('./fonts/Heebo-Bold.woff') format('woff');
    font-weight: bold;
    font-style: normal;
}

@font-face {
    font-family: 'Heebo';
    src: url('./fonts/Heebo-Thin.eot');
    src: local('Heebo-Thin'),
        url('./fonts/Heebo-Thin.eot?#iefix') format('embedded-opentype'),
        url('./fonts/Heebo-Thin.woff') format('woff'),
        url('./fonts/Heebo-Thin.ttf') format('truetype');
    font-weight: 100;
    font-style: normal;
}

$brand-color: #00ACE9;
$font-family: 'Heebo', sans-serif;
$block-border-radius: 40px;

$black: #333333;

$vhSize: 1080;

*{
	box-sizing: border-box;
}

body {
	position: relative;
	background-color: #fff;

    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
	
	font-family: $font-family;
	color: #000;
	font-weight: 400;
	line-height: 1.2;
	font-size: 16px;
	min-width: 320px;
	margin: 0;
}

html, body{
	height: 100%;
}

.wrapper{
	overflow: hidden;
	height: calc(100% - 48px - 16px - 16px);
	padding: 0 8px;
	display: flex;
	flex-wrap: wrap;	
}

.inner-col{
	display: flex;
	flex-direction: column;
	width: 100%;
	border-radius: 8px;
}

.col-4{
	width: calc(100% / 12 * 4);
	padding: 0 8px;
	height: 100%;
	display: flex;
}
.col-3{
	width: calc(100% / 12 * 3);
	padding: 0 8px;
	height: 100%;
	display: flex;
}
.col-5{
	width: calc(100% / 12 * 5);
	padding: 0 8px;
	height: 100%;
	display: flex;
}

@media (max-width: 1200px) {
	body{
		height: auto;
	}

	.wrapper{
		height: auto;
	}

	.col-4{
		width: calc(100% / 12 * 6);
	}
	.col-3{
		width: calc(100% / 12 * 6);
	}
	.col-5{
		width: 100%;
	}
}

@media (max-width: 992px) {
	.col-4{
		width: 100%;
	}
	.col-3{
		width: 100%;
	}
	.col-5{
		width: 100%;
	}
}

@function pxToVh($px) {
	@return ($px / $vhSize) * 100 + vh;
}
.chart{
    position: relative;    
    margin: 0 10%;
    &__content{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        text-align: center;
    }
    &__element{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        direction: ltr;
    }
    &__value{
        color: #353F66;
        font-size: pxToVh(60);
        font-weight: 500;
    }
    &__title{
        font-size: pxToVh(16);
        line-height: pxToVh(23);
        color: #D1D3D4;
    }
    &--big{
        height: 45.828vh;
        margin-bottom: pxToVh(24);
        >div{
            position: relative;
            height: 100%;
        }
        canvas{
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
    
        }
        div.chart__content{
            position: absolute; 
            height: auto;
        }
    }
    canvas{
        direction: ltr;
    }
    &--ltr{
        direction: ltr;
    }    
    // &--height{
    //     height: 38vh;
    // }
}

.chart-legend{
    list-style-type: none;
    margin: 0 -12px pxToVh(-14);
    padding: 0 10%;
    display: flex;
    flex-wrap: wrap;
    &--mt{
        margin-top: pxToVh(16);
    }
    &--center{
        justify-content: center;
        .chart-legend{
            &__item{
                margin: 0 15px;
            }
        }
    }
    &--two-colums{
        .chart-legend{
            &__item{
                width: 50%;
                padding: 0 12px;
            }
        }
    }
    &--random{
        .chart-legend{
            &__item{
                margin-left: 30px;
            }
        }
    }
    &__item{
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: pxToVh(14);
    }
    &__item-indicator{
        width: pxToVh(8);
        height: pxToVh(8);
        border-radius: 50%;
        flex-shrink: 0;
    }
    &__item-title{
        font-size: pxToVh(16);
        line-height: pxToVh(23);
        color: #9A9FB3;
        margin-right: 4px;
    }
    &__item-value{
        color: #353F66;
        font-size: pxToVh(20);
        font-weight: 500;
        margin-right: auto;
        width: 35px;
        text-align: right;
    }
}

.charts{
    display: flex;
    flex-wrap: wrap;
    margin-bottom: pxToVh(16);
    max-height: 55vh;
    overflow-y: auto;
    &__item{
        width: 50%;
        margin-bottom: 16px;

        .chart{
            max-width: 135px;
            margin: 0 auto;
            display: flex;
            position: relative;
            justify-content: center;
            &__value{
                font-size: pxToVh(20);
            }
            &__content{
                position: absolute;
            }
        }
        canvas{
            direction: ltr;
            max-height: 13.5vh;
        }
    }
    &__item-title{
        font-weight: bold;
        font-size: pxToVh(16);
        line-height: pxToVh(23);
        color: #353F66;
        margin-bottom: 8px;
        text-align: center;
    }
}

@media (max-width: 992px) {
    .chart{
        &--big{
            margin-bottom: pxToVh(32);
        }
    }

    .charts{
        &__item{
            width: 33.3333%;
        }
    }
}

@media (max-width: 768px) {
    .chart{
        &--big{
            height: 32.828vh;
        }
    }
}

.clock{
    text-align: center;
    width: 100%;
    padding: pxToVh(22) 0;
    &__live{
        font-size: pxToVh(60);
        font-weight: 500;        
        color: $brand-color;
    }
    &__title{
        font-size: pxToVh(20);
        line-height: pxToVh(29);
    }
}
.overlay{
    background-color: rgba(0,0,0,0.75);
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 9;
}
.form{
    position: fixed;
    top: 32px;
    left: 50%;
    transform: translateX(-50%);
    width: 992px;
    height: calc(100% - 62px);
    overflow-y: auto;
    background-color: #fff;
    z-index: 10;
    border-radius: 4px;
    &__header{
        display: flex;
        align-items: center;
        justify-content: space-between;
        background: linear-gradient(0deg, #F8FAFF, #F8FAFF), #F0FBFF;
        box-shadow: 0px 4px 25px rgba(0, 0, 0, 0.04);
        padding: pxToVh(24) 24px;
        margin-bottom: pxToVh(16);
        position: sticky;
        top: 0;
        right: 0;
        width: 100%;
    }
    &__header-logo{
        width: pxToVh(70);
        img{
            display: block;
            width: 100%;
        }
    }
    &__header-close-btn{
        width: pxToVh(25);
        cursor: pointer;
    }
    &__header-title{
        font-size: pxToVh(30);
        line-height: pxToVh(44);
    }
    &__body{
        padding: 0 24px pxToVh(24);
        border-bottom: 1px solid #DCE0E3;
        &:last-child{
            margin-bottom: 0;
            padding-bottom: 0;
        }
    }
    &__body-title{
        font-size: pxToVh(30);
        line-height: pxToVh(44);
        margin-bottom: pxToVh(16);
        font-weight: 500;
        padding-top: pxToVh(16);
    }
    &__row{
        display: flex;
        flex-wrap: wrap;
        margin: 0 -8px 24px;
    }
    &__col{
        width: 25%;
        padding: 0 8px;
    }
    &__group{
        background: #FFFFFF;
        box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.04);
        border-radius: 10px; 
        overflow: hidden;
        margin-bottom: 24px;
    }
    &__group-header{
        display: flex;
        align-items: center;
        justify-content: center;
        background: #409FFF;
        box-shadow: 0px 6px 6px rgba(0, 0, 0, 0.03);
        border-radius: 4px 4px 0px 0px;
        height: 35px;
        position: relative;
        .edit-btn__input{
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            right: 8px;
            border-radius: 4px;
            background-color: rgba(255, 255, 255, 0.9);
            border: none;
            height: 20px;
            line-height: 20px;
            padding: 0 6px;
            max-width: 75%;
            &:focus{
                outline: none;
            }
        }
    }
    &__group-header-title{
        text-align: center;
        color: #fff;
        font-size: 15px;
        line-height: 22px;
    }
    &__group-header-edit-btn{
        position: absolute;
        top: 50%;
        left: 8px;
        transform: translateY(-50%);
        display: flex;
        align-items: center;
        cursor: pointer;
    }
    &__group-body{
        padding: 10px 12px;
    }
    &__group-item{
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 6px;
        &:first-child{
            padding-bottom: 6px;
            border-bottom: 1px solid #DCE0E3;
        }
        &:nth-child(5){
            padding-bottom: 6px;
            border-bottom: 1px solid #DCE0E3;
        }
        &:last-child{
            margin-bottom: 0;
        }
    }
    &__group-item-title{
        font-size: 12px;
        line-height: 24px;
    }
    &__group-item-val{
        font-size: 12px;
        line-height: 24px;
        width: 34px;
        input{
            font-size: 12px;
            line-height: 24px;  
            width: 100%;
            border: 1px solid #D7E3F9;
            border-radius: 4px;
            height: 24px;
            line-height: 22px;
            text-align: center;
            direction: ltr;
            &:focus{
                outline: none;
            }
        }
    }
    &__footer{
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 40px;
        padding-bottom: 40px;
    }
    &__btn{
        width: 190px;
        margin: 0 10px;
        height: 40px;
        border-radius: 4px;
        font-size: 14px;
        border: none;
        cursor: pointer;
        text-align: center;
    }
    &__btn--blue{
        line-height: 40px;
        height: 40px;
        background: #409FFF;
        color: #fff;
    }
    &__btn--bordered{
        border: 1px solid #929BAA;
        line-height: 38px;
        color: #929BAA;
        background-color: transparent;
    }
    &__info-card-circle{
        width: 200px;
        height: 200px;
        border-radius: 50%;
        background: rgba(251, 97, 134, 0.1);
        border: 2px solid #FB6186;
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 0 auto;
    }
    &__info-card-circle-square{
        border: 1px solid #DCE7FA;
        border-radius: 4px;
        width: 100px;
        height: 100px;
        margin: 0 auto;
        input{
            width: 100%;
            background-color: transparent;
            border: none;
            text-align: center;
            font-size: 60px;
            line-height: 1;
            &:focus{
                outline: none;
            }
        }
    }
    &__info-card-title{
        font-weight: 700;
        font-size: 16px;
        line-height: 23px;
        text-align: center;
        padding-top: 12px;
    }
    &__info-card-title--blue{
        color: #00ACE9;
    }
    &__info-card-title--yellow{
        color: #FFDA23;
    }
}

.edit-btn{
    background: #409FFF;
    box-shadow: 0px 6px 6px rgba(0, 0, 0, 0.08);
    height: 35px;
    display: flex;
    align-items: center;
    position: relative;
    border-radius: 4px;
    padding: 0 8px;
    input{
        border-radius: 4px;
        background-color: rgba(255,255,255,0.9);
        border: none;
        height: 20px;
        line-height: 20px;
        padding: 0 6px;
        max-width: 75%;
        &:focus{
            outline: none;
        }
    }
    &__icon{
        width: 14px;
        height: 14px;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-right: auto;
        cursor: pointer;
    }
}

.header{
    background: linear-gradient(0deg, #F8FAFF, #F8FAFF), #F0FBFF;
    box-shadow: 0px 4px 25px rgba(0, 0, 0, 0.04);
    height: 48px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 16px;
    margin-bottom: 16px;
    &__logo{
        width: 70px;
        display: block;
        img{
            display: block;
            width: 100%;
        }
    }
    &__company{
        font-size: pxToVh(20);
        line-height: pxToVh(29);
        text-decoration: none;
        span{
            color: $brand-color;
        }
        color: $black;
    }
    &__btn{
        background: #409FFF;
        border-radius: 4px;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 0 30px;
        color: #fff;
        height: 44px;
        img{
            margin-right: 10px;
        }
    }
}

@media (max-width: 768px) {
    .header{
        &__company{
            display: none;
        }
    }
}

.info{
    display: flex;
    flex-wrap: wrap;
    margin: 0 -8px;
    &__col{
        width: 50%;
        padding: 0 8px;
        display: flex;
        flex-direction: column;
    }
}

.info-card{
    background: #fff;
    box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.04);
    border-radius: 10px;
    padding: pxToVh(32) 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-direction: column;
    margin-bottom: 16px;
    flex-grow: 1;
    &:last-child{
        margin-bottom: 0;
    }
    &__title{
        font-weight: 500;
        font-size: pxToVh(24);
        line-height: pxToVh(35);
    }
    &__value{
        font-weight: 500;
        font-size: pxToVh(60);
    }
    &__date{
        color: #D1D3D4;
        font-size: pxToVh(16);
        line-height: pxToVh(23);    
    }
    &--blue{
        .info-card{
            &__value{
                color: #00ACE9;
            }
        }
    }
    &--yellow{
        .info-card{
            &__value{
                color: #FFDA23;
            }
        }
    }
    &--pink{
        .info-card{
            &__value{
                color: #FB6186;
            }
        }
    }
    &--big{
        .info-card{
            &__value{
                background: rgba(251, 97, 134, 0.1);
                border: 2px solid #FB6186;
                width: pxToVh(200);
                height: pxToVh(200);
                display: flex;
                align-items: center;
                justify-content: center;
                border-radius: 50%;
            }
        }
    }
}

.panel{
    background: #fff;
    box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.04);
    border-radius: 10px;
    margin-bottom: 16px;
    padding: pxToVh(32) 0;
    display: flex;
    &:last-child{
        margin-bottom: 0;
    }
    &--no-pd{
        padding: 0;
    }
    &--flex{
        display: flex;
    }
    &--contnet-between{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    &--grow{
        flex-grow: 1;
    }
    &--55{
        height: 50%;
    }
    &__header{
        text-align: center;
        font-weight: 500;
        font-size: pxToVh(24);
        line-height: pxToVh(35);
        margin-bottom: pxToVh(16);
    }
    &__inner{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        width: 100%;
    }
}

.logo{
    width: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.04);
    border-radius: 10px;
    img{
        max-width: 80%;
        width: pxToVh(175);
    }
}


.table{
    padding: 0 10%;
    width: 100%;
    th{
        font-size: pxToVh(16);
        line-height: pxToVh(23);
        color: #D1D3D4;
        padding-bottom: pxToVh(16);
        font-weight: 500;
        &:nth-child(1){
            text-align: right;
            width: 50%;
        }
        &:nth-child(2){
            width: 25%;
        }
        &:nth-child(3){
            width: 25px;
        }
        &:nth-child(2), &:nth-child(3){
            text-align: center;
        }
    }
    td{
        padding: pxToVh(4);
        font-size: pxToVh(16);
        line-height: pxToVh(23);
        color: #353F66;
        font-weight: 400;
        border-bottom: 1px solid #F1F3F7;
        &:nth-child(2){
            color: #00ACE9;
            font-weight: 500;
            text-align: center;
        }
        &:nth-child(3){
            color: #FB6186;
            font-weight: 500;
            text-align: center;
        }
    }
    tbody{
        tr{
            &:last-child{
                td{
                    padding-bottom: 0;
                    border: none;
                }
            }
        }
    }
}

@media (max-width: 1200px) {
    .table{
        margin-top: pxToVh(16);
    }
}
</style>
