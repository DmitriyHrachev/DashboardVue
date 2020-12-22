
<template>
<div>
  <div class="overlay"></div>
<form class="form">
	<div class="form__header">
		<div v-on:click="close" class="form__header-close-btn">
			<img src="../../assets/close.svg" alt="">
		</div>
		<div class="form__header-title">הזנת נתונים</div>
		<div class="form__header-logo">
			<img src="../../assets/logo.svg" alt="">
		</div>
	</div>
	<div class="form__body">
		<div class="form__body-title">
			נוכחות
		</div>
		<div class="form__row">
			<div class="form__col" v-for="group in groups" v-bind:key="group.id">
				<GroupCard v-bind:group="group" v-on:changeGroup="changeGroup" v-on:changeEdit="changeGroupEdit" v-on:changeName="changeGroupName" />
			</div>
			<div class="form__col">
				<div class="edit-btn">
					<input type="text" placeholder="הזן שם הקבוצה..." v-model="newGroupName" class="edit-btn__input">
					<img src="../../assets/add-icon.svg" alt=""  v-on:click="addGroup" class="edit-btn__icon">
				</div>
			</div>
		</div>
	</div>
	<div class="form__body">
		<div class="form__body-title">
			נתונים יבשים
		</div>
		<div class="form__info-cards">
			<div class="form__info-cards-col">
				<div class="form__info-card">
					<input v-model="infoCard" placeholder="הזן נושה..." class="form__info-card-title-input" type="text">
					<div class="form__info-card-circle">
						<div class="form__info-card-circle-square">
							<div class="form__info-card-title">הזן נושה</div>
							<input v-model="infoCardVal" placeholder="..."  type="text">
						</div>
					</div>
				</div>
			</div>
			<div class="form__info-cards-col">
				<div class="form__info-card">
					<input v-model="infoCard2" placeholder="הזן נושה..." class="form__info-card-title-input" type="text">
					<div class="form__info-card-circle">
						<div class="form__info-card-circle-square">
							<div class="form__info-card-title">הזן נושה</div>
							<input v-model="infoCardVal2" placeholder="..."  type="text">
						</div>
					</div>
				</div>
				<div class="form__info-card">
					<input v-model="infoCard3" placeholder="הזן נושה..." class="form__info-card-title-input" type="text">
					<div class="form__info-card-circle">
						<div class="form__info-card-circle-square">
							<div class="form__info-card-title">הזן נושה</div>
							<input v-model="infoCardVal3" placeholder="..."  type="text">
						</div>
					</div>
				</div>
			</div>
		</div>
		<!-- <div class="form__row">
			<div class="form__col">
				
				
			</div>
			<div class="form__col">
				<input v-model="infoCard2" type="text">
				<input v-model="infoCardVal2" type="text">
			</div>
			<div class="form__col">
				<input v-model="infoCard3" type="text">
				<input v-model="infoCardVal3" type="text">
			</div>
		</div> -->
	</div>
	<div class="form__footer">
		<div v-on:click="submitForm" :class="{form__disabled: !isSubmitAllowed}" class="form__btn form__btn--blue">שמור שינויים</div>
		<div v-on:click="close" class="form__btn form__btn--bordered">בטל שינויים</div>
	</div>
</form>

</div>
</template>

<script>
import GroupCard from './GroupCard.vue';
export default {
  components: { GroupCard },  
  data () {
    return {
	  newGroupName: '',
	  infoCard: '',
	  infoCard2: '',
	  infoCard3: '',
	  infoCardVal: '',
	  infoCardVal2: '',
	  infoCardVal3: '',
	  isSubmitAllowed: false,
      groups: [],
      close: () => {
          const vm = this;
          vm.$emit('closeModal');
      },
      save: () => {
          const vm = this;
          vm.$emit('saveModal');
      },
      addGroup: () => {
          if(!this.newGroupName) {
              this.newGroupName = 'גליל'
          }
          const group = {
			  id: this.ID(),
              studentsAmount: '',
              offStudy: '',
              activity: '',
              ill: '',
              banned: '',
              inCampus: '',
              onStudy: '',
              groupName: this.newGroupName,
			  edit: false,
			  isError: false
          }
          this.groups = [...this.groups, group];
          this.newGroupName = '';
	  },
	  changeGroupEdit: (id) => {
		  const index = this.groups.findIndex((item) => item.id === id);
		  this.groups[index].edit = true;
	  },
	  changeGroupName: (data) => {
		  let index = this.groups.findIndex((item) => item.id === data.id);
		  this.groups[index].groupName = data.groupName;
		  this.groups[index].edit = false;
		  this.groups = [...this.groups];
	  },
	  changeGroup: (data) => {
		  const index = this.groups.findIndex((item) => item.id === data.id);
		  const newData = {
	      activity : data.activity,
		  banned : data.banned,
		  ill : data.ill,
		  inCampus : data.inCampus,
		  offStudy : data.offStudy,
		  onStudy : data.onStudy,
		  studentsAmount : data.studentsAmount ,
		  isError: data.isError,
		  }
		this.groups[index] = {...this.groups[index], ...newData}
		const arr = this.groups.filter(group => group.isError);
		if(arr && arr.length) {
			this.isSubmitAllowed = false;
			return;
		}
		this.isSubmitAllowed = true;  
	  },
	  ID:() => {
  		return '_' + Math.random().toString(36).substr(2, 9);
	  },
	  submitForm: () => {
		  this.$emit('cardValues', {
			  infoCard: {
				  name: this.infoCard,
				  value: this.infoCardVal
			  },
			  infoCard2: {
				  name: this.infoCard2,
				  value: this.infoCardVal2
			  },
			  infoCard3: {
				  name: this.infoCard3,
				  value: this.infoCardVal3
			  }
		  })
		  const errorEl = this.groups.filter(group => group.isError);
		  if(!errorEl.length) {
		  	this.$emit('submitForm', [ ...this.groups]);
		  	this.$emit('closeModal');
		  }
	  }
    }
  }
  
}
</script>

<style lang="scss">
	.form__info-cards{
		display: flex;
		justify-content: center;
	}
	.form__info-cards-col{
		width: 40%;
		margin: 0 5%;
		display: flex;
		flex-direction: column;
	}
	.form__info-card{
		background: #FFFFFF;
		box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.04);
		border-radius: 10px;
		display: flex;
		flex-direction: column;
		padding: 25px;
		margin-bottom: 5%;
		height: 100%;
		&:last-child{
			margin-bottom: 0;
		}
	}
	.form__info-card-title-input{
		border: 1px solid #D7E3F9;
		height: 32px;
		line-height: 30px;
		padding: 0 10px;
		max-width: 270px;
		display: block;
		margin: 0 auto 25px;
	}
	.form__info-card-circle-square{
		width: 100px;
		height: 100px;
	}
	.form__info-card-title{
		font-weight: 500;
		font-size: 16px;
		line-height: 23px;
		text-align: center;
	}
</style>
