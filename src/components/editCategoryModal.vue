<template>
  <div id="cat-edit-modal" class="ui small modal">
  	<i class="close icon"></i>
  	<div class="header">
  		编辑标签
  	</div>
  	<div class="content">
  		<form class="ui form">
  			<div class="field">
  				<label>标签</label>
  				<input type="text" placeholder="请输入标签名字" v-model="catName">
  			</div>
  			<div class="field">
  				<label>标签颜色</label>
  				<select class="ui simple dropdown" v-model="catColor">
  					<option value="">请选择</option>
  					<option value="{{color}}" v-for="(key, color) in categoryColors">
  						{{ key }}
  					</option>
  				</select>
  			</div>
  		</form>
  	</div>
  	<div class="actions">
      <button class="ui inverted blue button" @click="editCategory">保存 </button>
  	</div>
  </div>
</template>

<script>
import store from '../store'
export default {
  props:['category_name'],
  data() {
  	return {
  		catName: '',
  		catColor: '',
  		categoryColors: {
        '红色': 'red',
        '橙色': 'orange',
        '黄色': 'yellow',
        '黄绿色': 'olive',
        '绿色': 'green',
        'Teal': 'teal',
        '蓝色': 'blue',
        '深紫色': 'violet',
        '紫色': 'purple',
        '粉色': 'pink',
        '棕色': 'brown',
        '灰色': 'grey',
        '黑色': 'black'
      }
  	}
  },
  methods: {
  	editCategory () {
  		var editedCategory = {};
      editedCategory[this.catName] = this.catColor;
  		store.editCategory(editedCategory, this.catName, this.category_name)
  		$('#cat-edit-modal').modal('hide');
  	}
  },
  events: {
  	'edit-category': function(name, color) {
      this.catName = name;
      this.catColor = color;
  		$('#cat-edit-modal').modal('show');
  	}
  }
}
</script>
