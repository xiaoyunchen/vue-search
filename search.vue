<template>
	<div class="searchContainer" v-show="show" :transition="transtionModel">
		<div class="weui_mask" v-on:click="show=false">

		</div>
		<div class="searchWrapper">
			<div class="searchHeader weui_search_inner">
				<label v-text="label"></label>
				<input class="weui_search_input" v-model="query" :placeholder="inputholder" />
				<a v-show="query.length>0" transition="fade" href="javascript:" class="weui_icon_clear" v-on:click="query=''"></a>
			</div>
			<div class="searchList">
				<ul>
					<li v-text="item[displaykey]" v-on:click="chooseItem(item)" v-for="item in items | filterBy query | limitBy limit" transition="staggered" stagger="50">
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
	import 'weui';
	export default{
		name:'search',
		props: {
			show:{
				type:Boolean,
				default:false
			},
			items: {		//搜索数组
				type: Array,
				required: true
			},
			displaykey:{		//对象显示字段，默认为text
				type:String,
				default:'text'
			},
			limit:{		//最大显示列表数量
				type:Number,
				default:10
			},
			label:{		//标签文字
				type:String,
				default:'搜索'
			},
			inputholder:{	//搜索框placeholder
				type:String,
				default:'搜索'
			},
			transtionModel:{		//动画transtion模式，自定义该属性时需要自行实现对应CSS
				type:String,
				default:'slide'
			}
		},
		data: function() {
			return {
				query: ''   // 搜索字段
			};
		},
		methods: {		//用户选择后进行事件派发
			chooseItem: function(item) {
				//派发事件
				this.$dispatch('fullscreensearch',item);
			}
		}
	}

</script>

<style scoped>
	.searchContainer{
		position: fixed;
		width: 100%;
		height: 100%;
		z-index: 9999;
		top:0;
	}
	.searchWrapper{
		position: relative;
		z-index: 9999;
		background-color: #FFFFFF;
		padding-top: 10px;
		font-size: 15px;
	}
	.searchHeader{
		padding-left: 0;
	}
	.searchHeader label{
		position: absolute;
		left: 15px;
		color: #607786;
		line-height: 28px;
	}
	.searchList{
		padding:0 10px 15px 90px;
	}
	.searchHeader .weui_search_input{
		-webkit-appearance: none;
		border-radius: 0;
		border-bottom: 1px solid #d6e4ed;
		font-size: 15px;
		padding-left: 90px;
	}
	ul {
		padding-left: 0;
		font-family: Helvetica, Arial, sans-serif;
	}
	.searchList li{
		padding: 8px 0;
		font-size:16px;
		border-bottom: 1px solid #d6e4ed;
	}
	.staggered-transition {
		transition: all .3s ease;
		overflow: hidden;
		margin: 0;
	}
	.staggered-enter, .staggered-leave {
		opacity: 0;
		height: 0;
	}
</style>
<style>
	.slide-transition{
		top: 0;
		transform: translateY(0);
		-webkit-transform: translateY(0);
		visibility: visible;
		transition: all 0.3s ease-out;
	}
	.slide-enter,.slide-leave{
		transform: translateY(100%);
		-webkit-transform: translateY(100%);
		visibility: hidden;
	}
	.fade-transition{
		transition: all 0.3s ease-out;
		visibility: visible;
	}
	.fade-enter,.fade-leave{
		visibility: hidden;
	}
</style>