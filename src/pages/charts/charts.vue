
<template>
  <div id="charts" :style="style">
   
  </div>
</template>

<script type="text/javascript">
	import {mapState, mapActions} from 'vuex'
	import Mock from 'mockjs'

	export default {
		data() {
			return {
				//echarts实例
				chart: "" ,
				option: {
				    xAxis: {
				        type: 'category',
				        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
				    },
				    yAxis: {
				        type: 'value'
				    },
				    series: [{
				        data: [820, 932, 901, 934, 1290, 1330, 1320],
				        type: 'line'
				    }]
				}
			};
		},
		computed: {
			style() {
				return {
					height: '300px',
					width: '100%'
				};
			}
		},
		mounted() {
		  this.init();
		  this.SetTimeoutOne()
		  this.websocket()
		},
		watch: {
			//观察option的变化
			option: {
				handler(newVal, oldVal) {
					if (this.chart) {
						if (newVal) {
							this.chart.setOption(newVal);
						} else {
							this.chart.setOption(oldVal);
						}
					} else {
						this.init();
					}
				},
				deep: true //对象内部属性的监听，关键。
			}
		},
		methods: {
			init() {
				window.addEventListener("resize", this.chart.resize);
				this.chart = this.$echarts.init(document.getElementById('charts'));
				this.chart.setOption(this.option);
			 },
			 MockData(){
			 	var temp = []
			 	var data = Mock.mock({
			 		'list|7': [{
				        'a|1-100': 1
				    }]

				})
				data.list.map((Item,Idx)=>{
					temp.push(Item.a)
				})
				this.option.series[0].data = temp
				this.SetTimeoutOne()
			 },
			 SetTimeoutOne(){
			 	setTimeout(()=> {
				  	this.MockData()
				 }, 2000);
			 },
			 websocket() {
                let ws = new WebSocket('ws://172.17.127.164:8000/websocket');
                ws.onopen = () => {
                    // Web Socket 已连接上，使用 send() 方法发送数据
                    console.log('数据发送中...')
                    ws.send('Holle')
                    console.log('数据发送完成')
                }
                ws.onmessage = evt => {
                     console.log('数据已接收...')
                }
                ws.onclose = function () {
                    // 关闭 websocket
                    console.log('连接已关闭...')
                }
                // 路由跳转时结束websocket链接
                this.$router.afterEach(function () {
                    ws.close()
                })
            }
		},
		components: {
			
		}
	}
</script>

