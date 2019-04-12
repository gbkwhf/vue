
<template>
    <div>
        <h1>1.data定义的属性不会因为它的赋值变量的变化而变化</h1>
        <span>{{num1}}</span>
        <button @click="num1Click">查看num1值</button>
        <hr>
        <h1>2.computed定义的属性会随它的赋值变量的变化而变化</h1>
        <span>{{c_num1}}</span>
        <button @click="c_num1Click">查看c_num1值</button>
        <hr>
        <button @click="outerNumChange">变量值+10</button>
    </div>
</template>

<script>
    let mm = {'no': 30};
    export default{
        data(){
            return {
                t: mm,//这样会导致这个组件被多次使用时，c_num1共享状态。
                num1: mm.no
            }
        },
        computed: {
            c_num1(){
                return mm.no
            }
        },
        methods: {
            num1Click(){
                console.log('num1 from 30 to:', this.num1);
            },
            c_num1Click(){
                console.log('c_num1 from 30 to:', this.c_num1);
            },
            outerNumChange(){
                mm.no += 10;
                console.log(mm.no);
            }
        }
    }
</script>

<style>
</style>






























<!--<template>
	<div id="app">
		<table id="cartTable">
			<thead>
				<tr>
					<th><label><input class="check" v-model="checked" v-on:click="allSelect" type="checkbox"/> 全选</label></th>
					<th>商品</th>
					<th>单价</th>
					<th>数量</th>
					<th>小计</th>
					<th>操作</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="(item, index) in list">
					<td class="checkbox">
						<input class="check-one check" type="checkbox" v-model='checklist' :value="item.id" />
					</td>
					<td class="goods">
						<img :src=item.image alt="" />
						<span>{{item.name}}</span>
					</td>
					<td class="price">{{item.price}}</td>
					<td class="count">
						<span v-show="item.count>1" class="reduce" v-on:click="reducehanlder(index)">-</span>
						<input class="count-input" type="text" v-model="item.count" />
						<span class="add" v-on:click="addhandler(index)">+</span>
					</td>
					<td class="subtotal">{{item.subtotal * item.count}}</td>
					<td class="operation">
						<span v-on:click="deletehandle(index)">删除</span>
					</td>
				</tr>

			</tbody>
		</table>
		<div class="foot" id="foot">
			<label class="fl select-all"><input type="checkbox" class="check" v-model="checked" v-on:click="allSelect"/> 全选</label>
			<div class="fl" v-on:click="alldel">删除</div>
			<div class="fr closing">结 算</div>
			<div class="fr total">合计：￥<span>{{priceTotal}}</span></div>
			<div class="fr selected" id="selected">已选商品<span id="selectedTotal">{{this.count}}</span>件</div>
		</div>
	</div>
	</div>
</template>
<style type="text/css">
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
	
	* {
		margin: 0;
		padding: 0;
	}
	
	a {
		color: #666;
		text-decoration: none;
	}
	
	body {
		padding: 20px;
		color: #666;
	}
	
	.fl {
		float: left;
	}
	
	.fr {
		float: right;
	}
	
	table {
		border-collapse: collapse;
		border-spacing: 0;
		border: 0;
		text-align: center;
		/*width: 937px;*/
		width: 100%;
	}
	
	th,
	td {
		border: 1px solid #CADEFF;
	}
	
	th {
		background: #e2f2ff;
		border-top: 3px solid #a7cbff;
		height: 30px;
	}
	
	td {
		padding: 10px;
		color: #444;
	}
	
	tbody tr:hover {
		background: RGB(238, 246, 255);
	}
	
	.checkbox {
		width: 60px;
	}
	
	.goods {
		width: 200px;
	}
	
	.goods span {
		width: 180px;
		margin-top: 20px;
		text-align: left;
		float: left;
	}
	
	.price {
		width: 130px;
	}
	
	.count {
		width: 90px;
	}
	
	.count .add,
	.count input,
	.count .reduce {
		float: left;
		margin-right: -1px;
		position: relative;
		z-index: 0;
	}
	
	.count .add,
	.count .reduce {
		height: 23px;
		width: 17px;
		border: 1px solid #e5e5e5;
		background: #f0f0f0;
		text-align: center;
		line-height: 23px;
		color: #444;
	}
	
	.count .add:hover,
	.count .reduce:hover {
		color: #f50;
		z-index: 3;
		border-color: #f60;
		cursor: pointer;
	}
	
	.count input {
		width: 50px;
		height: 15px;
		line-height: 15px;
		border: 1px solid #aaa;
		color: #343434;
		text-align: center;
		padding: 4px 0;
		background-color: #fff;
		z-index: 2;
	}
	
	.subtotal {
		width: 150px;
		color: red;
		font-weight: bold;
	}
	
	.operation {
		width: 80px;
	}
	
	.operation span:hover,
	a:hover {
		cursor: pointer;
		color: red;
		text-decoration: underline;
	}
	
	img {
		width: 100px;
		height: 80px;
		/*    border: 1px solid #ccc;
*/
		margin-right: 10px;
		float: left;
	}
	
	.foot {
		width: 935px;
		margin-top: 10px;
		color: #666;
		height: 48px;
		border: 1px solid #c8c8c8;
		background-color: #eaeaea;
		background-image: linear-gradient(RGB(241, 241, 241), RGB(226, 226, 226));
		position: relative;
		z-index: 8;
	}
	
	.foot div,
	.foot a {
		line-height: 48px;
		height: 48px;
	}
	
	.foot .select-all {
		width: 100px;
		height: 48px;
		line-height: 48px;
		padding-left: 5px;
		color: #666;
	}
	
	.foot .total {
		margin: 0 20px;
		cursor: pointer;
	}
	
	.foot #priceTotal,
	.foot #selectedTotal {
		color: red;
		font-family: "Microsoft Yahei";
		font-weight: bold;
	}
</style>
<script>
	export default {
		data() {
				return {
					list: [{
						id: 1,
						name: 'Casio/卡西欧 EX-TR350',
						price: 5999.88,
						count: 1,
						subtotal: 5999.88
						
					}, {
						id: 2,
						name: 'Canon/佳能 PowerShot SX50 HS',
						price: 3888.50,
						count: 1,
						subtotal: 3888.50
					
					}, {
						id: 3,
						name: 'Sony/索尼 DSC-WX300',
						price: 1428.50,
						count: 1,
						subtotal: 1428.50
						
					}, {
						id: 4,
						name: 'Fujifilm/富士 instax mini 25',
						price: 640.60,
						count: 1,
						subtotal: 640.60
						
					}],
					count: 0, //总个数
					checked: false, //默认未全选中
					checklist: [] //选中的id列表
				}
			},
			methods: {
				//全选
				allSelect() {
					if(this.checked) {
						this.checklist = [];
					} else {
						this.checklist = [];
						for(var i = 0; i < this.list.length; i++) {
							var item = this.list[i];
							this.checklist.push(item.id);
						}
					}

				},
				deletehandle(index) {
					this.list.splice(index, 1);
				},
				reducehanlder(index) {
					this.list[index].count--
				},
				addhandler(index) {
					this.list[index].count++
				},
				alldel() {
					if(this.checked) {
						this.list = [];
						this.checklist = [];
						// this.checked = false;
					} else {
						alert('请全部选中');
					}
				},

				//若选中的列表同数据列表长度相等 改变全选的状态 
				selectchange() {
					if(this.checklist.length == this.list.length) {
						this.checked = true;
					} else {
						this.checked = false;
					}
				}

			},
			computed: {

				//合计
				priceTotal() {
					this.selectchange();
					var total = 0;
					this.count = 0;
					for(var i = 0; i < this.list.length; i++) {
						var item = this.list[i];
						//判断当前id 是否存在checklist 则做计算
						if(this.checklist.indexOf(item.id) >= 0) {
							total += (parseFloat(item.price) *1* item.count);
							this.count += item.count;
						}
						
					}
					
					return total.toString().replace(/\B (?= (\d{3} )+$)/g, ',');
				}

			},
	}
</script>-->