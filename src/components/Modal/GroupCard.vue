
<template>
	<div class="form__group">
		<div class="form__group-header">
			<div v-if="!group.edit" class="form__group-header-title">{{group.groupName}}</div>
			<input v-if="group.edit" type="text" placeholder="הזן שם הקבוצה..." v-model="newGroupName" class="edit-btn__input">
			<div v-on:click="editActive" class="form__group-header-edit-btn">
				<img src="../../assets/edit-icon.svg" alt="">
			</div>				
		</div>
		<div class="form__group-body">
			<div class="form__group-item">
				<div class="form__group-item-title">סה״כ חניכים בקבוצה</div>
				<div class="form__group-item-val">
					<input type="text" :class="{required: isError}" :required="checkFields('studentsAmount')" v-on:keyup="updateData" v-model="studentsAmount">
					<!-- <input type="text" v-on:keyup="updateData" v-model="studentsAmount"> -->
				</div>
			</div>

			<div class="form__group-item">
				<div class="form__group-item-title">בחופשה</div>
				<div class="form__group-item-val">
					<input type="text" v-on:keyup="updateData" v-model="offStudy">
				</div>
			</div>
			<div class="form__group-item">
				<div class="form__group-item-title">בפעילות חוץ כפרית</div>
				<div class="form__group-item-val">
					<input type="text" v-on:keyup="updateData" v-model="activity">
				</div>
			</div>
			<div class="form__group-item">
				<div class="form__group-item-title">בטיפול רפואי חוץ</div>
				<div class="form__group-item-val">
					<input type="text" v-on:keyup="updateData" v-model="ill">
				</div>
			</div>
			<div class="form__group-item">
				<div class="form__group-item-title">מושהים</div>
				<div class="form__group-item-val">
					<input type="text" v-on:keyup="updateData" v-model="banned">
				</div>
			</div>

			<div class="form__group-item">
				<div class="form__group-item-title">נמצאים בכפר</div>
				<div class="form__group-item-val">
					{{  inCampusCount }}
				</div>
			</div>
			<div class="form__group-item">
				<div class="form__group-item-title">הגיעו לבית הספר</div>
				<div class="form__group-item-val">
					<input type="text" :class="{required: isError}" :required="checkFields('onStudy')" v-on:keyup="updateData" v-model="onStudy">
					<!-- <input type="text"  v-on:keyup="updateData" v-model="onStudy"> -->
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {  
  props: ['group'],
  computed: {
	  inCampusCount() {
		  this.inCampus = parseInt(this.studentsAmount || 0) - parseInt(this.offStudy || 0) - parseInt(this.activity || 0) - parseInt(this.ill || 0) - parseInt(this.banned || 0)
		  return this.inCampus;
	  }
  },

  data () {
    return {
		isError: false,
		studentsAmount: '',
		offStudy: '',
		activity: '',
		ill: '',
		banned: '',
		inCampus: '',
		onStudy: '',
		groupName: this.newGroupName,
        newGroupName: '',
        editActive: () => {
            if(!this.group.edit) {
                this.group.edit = true;
                return;
			}
			this.group.edit = false;
			this.$emit('changeName', {id: this.group.id, groupName: this.newGroupName});
            
		},
		checkFields: (name) => {
			const data = this[name];
			if(data !== '' && parseInt(data) !== 0) {
				return false;
			}
			return true
		},
        updateData: () => {
        const newGroupData = {
              studentsAmount: this.studentsAmount,
              offStudy: this.offStudy,
              activity: this.activity,
              ill: this.ill,
              banned: this.banned,
              inCampus: this.inCampus,
			  onStudy: this.onStudy,
			  isError: this.isError
			}
			if(!this.checkFields('studentsAmount') && !this.checkFields('onStudy')) {
				this.isError = false;
				const data = {...this.group, ...newGroupData, isError: false}
				this.$emit("changeGroup", data);
				return;
			}              
			this.isError =  true;
			const data = {...this.group, ...newGroupData, isError: true}
			this.$emit("changeGroup", data)
		}
    }
  }
}
</script>

<style lang="scss">

</style>
