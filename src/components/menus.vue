<template>
	<div>

		<b-modal ref="myModalRef" hide-footer title="Using Component Methods">
	    <div class="d-block text-center">
	      <b-form-input v-model="newText"
                  type="text"
                  placeholder="输入事项名称" @keyup.enter="addItem"></b-form-input>！
	    </div>
	    <b-btn class="mt-3" variant="outline-danger" block @click="hideModal">确定</b-btn>
	  </b-modal>
		<b-list-group>

			<b-list-group-item href="#" class="list-style"  @click='goList("all")'>
		  	我的一天
		  </b-list-group-item>

		  <b-list-group-item href="#" class="list-style" v-for="list in lists" @click="goList(list.title)">
		  	{{ list.title }}
		  </b-list-group-item>

		  <b-list-group-item href="#">
		  	<input type="text" v-model="newtitle" name="" v-if="isAdd" @keyup.enter="addList">
		  </b-list-group-item>

		  <b-list-group-item href="#" class="list-style" @click="isAdd = true">
		  	+新建清单
		  </b-list-group-item>

		</b-list-group>
	</div>
</template>

<script>
import bus from '../assets/eventBus'

export default{
	data() {
		return {
			name: 'lj',
			newtitle: '',
			isAdd: false
		}
	},
	computed: {
		lists() {
			return this.$store.getters.lists;
		}
	},
	methods: {
		addList() {
			let newList = {
				title: this.newtitle,
				count: 0
			}
			this.$store.commit('addList', newList)
			this.newtitle = "";
			this.isAdd = false
		},
		goList(title) {
      bus.$emit('LIstTitle', title)
    }
	}
}

</script>

<style>
.list-style {
	background: #283643;
	color: #fff;
}


</style>
