<template>
    <div>
        <div class="key-input" v-show="inputing" @click="inputing=false">{{num | formatMoney}}</div>
        <input class="key-input" v-model.number="num" placeholder="1元起投" v-show="!inputing" @blur="changeInput" v-money>
    </div>
</template>


<script>


	export default {
		data() {
			return {
				num: '',
				inputing:false
			}
		},
		directives: {
			money: {
				bind: function (el) {
					el.handler = function (e) {
						var key = {
							'0': true,
							'1': true,
							'2': true,
							'3': true,
							'4': true,
							'5': true,
							'6': true,
							'7': true,
							'8': true,
							'9': true,
							'.': true,
							'Backspace': true
						}
						if (!key[e.key]) {
							// console.log(e.key)
							// e.stopPropagation();
							e.preventDefault()
						} else {
							// console.log(e.key)
							let index = el.value.split('.');
							if (index.length > 1 && index[1].length >= 2 && e.key != 'Backspace') {
								e.preventDefault()
							}
						}
					}
					el.addEventListener('keydown', el.handler)
				},
				unbind: function (el) {
					el.removeEventListener('keydown', el.handler)
				}
			}
		}
	}
</script>


<style scoped lang="less">
    .key-input{
        width:3rem;
        vertical-align:6px;
        border:none;
        padding:0;
        height:28px;
        line-height:28px;
        padding-left:.013rem;
        font-size:26px;
        color:#DAA551
    }
</style>
