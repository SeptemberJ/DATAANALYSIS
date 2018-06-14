<template>
	<div class="layout">
        <Layout>
            <Sider :style="{height:'100vh',position:'fixed'}" ref="side1" hide-trigger collapsible :collapsed-width="78" v-model="isCollapsed">
                <Menu active-name="1-2" theme="light" width="auto" :class="menuitemClasses">
                    <MenuItem name="1-1">
                        <Icon type="ios-navigate"></Icon>
                        <span>用户分析</span>
                    </MenuItem>
                    <MenuItem name="1-2">
                        <Icon type="settings"></Icon>
                        <span>设备分析</span>
                    </MenuItem>
                </Menu>
            </Sider>
            <Layout :style="{position:'relative',left:isCollapsed?'78px':'200px'}">
                <Header :style="{padding: 0}" class="layout-header-bar">
                    <Icon @click.native="collapsedSider" :class="rotateIcon" :style="{margin: '20px 20px 0'}" type="navicon-round" size="24"></Icon>
                    <div :style="{float: 'right',marginRight:isCollapsed?'78px':'200px'}">
	                    <Button @click="" type="text">
	                        TEST
	                        <Icon type="power" size="14"></Icon>
	                        退出
	                    </Button>
                    </div>
                </Header>
                <Content :style="{margin: '20px', background: '#fff', minHeight: '260px'}">
                    Content
                </Content>
            </Layout>
        </Layout>
    </div>
    
	<!-- <div class="LoginWrap">
		<div>
			<Button type="primary">Primary</Button>
		</div>
	</div> -->
	<!-- <div class="db_login">
		<div class="db_login_top"><a href="javascript:void(0);" class="cancel" @click="goBack">取消</a>登录豆瓣</div>
		<div class="db_login_form">
			<form action="#" method="post">
				<p class="form_item"><input type="text" name="username" placeholder="邮箱/手机号/用户名"></p>
				<p class="form_item"><input type="password" name="pasword" placeholder="密码"></p>
				<p class="form_btn"><button type="submit">登录</button></p>
			</form>
		</div>
		<div class="login_other">使用其它方式登录 & 找回密码</div>
		<div class="regist_download">
			<a href="#">注册豆瓣</a><a href="#">下载豆瓣App</a>
		</div>
	</div> -->
</template>
<script type="text/javascript">
	export default {
		data () {
            return {
                isCollapsed: false
            }
        },
        computed: {
            rotateIcon () {
                return [
                    'menu-icon',
                    this.isCollapsed ? 'rotate-icon' : ''
                ];
            },
            menuitemClasses () {
                return [
                    'menu-item',
                    this.isCollapsed ? 'collapsed-menu' : ''
                ]
            }
        },
		methods: {
			goBack(){
				this.$router.go(-1);
			},
			collapsedSider () {
                this.$refs.side1.toggleCollapse();
            }
		}
	}
</script>
<style scoped>
	::-webkit-scrollbar{
	  display:none;
	}
	.layout{
        border: 1px solid #d7dde4;
        background: #f5f7f9;
        position: relative;
        border-radius: 4px;
        overflow: hidden;
    }
    .ivu-layout-sider{
    	background: #fff !important;
    }
    .layout-header-bar{
    	width: 100%;
    	position: fixed;
        background: #fff;
        box-shadow: 0 1px 1px rgba(0,0,0,.1);
    }
    .layout-logo-left{
        width: 90%;
        height: 30px;
        background: #5b6270;
        border-radius: 3px;
        margin: 15px auto;
    }
    .menu-icon{
        transition: all .3s;
    }
    .rotate-icon{
        transform: rotate(-90deg);
    }
    .menu-item span{
        display: inline-block;
        overflow: hidden;
        width: 69px;
        text-overflow: ellipsis;
        white-space: nowrap;
        vertical-align: bottom;
        transition: width .2s ease .2s;
    }
    .menu-item i{
        transform: translateX(0px);
        transition: font-size .2s ease, transform .2s ease;
        vertical-align: middle;
        font-size: 16px;
    }
    .collapsed-menu span{
        width: 0px;
        transition: width .2s ease;
    }
    .collapsed-menu i{
        transform: translateX(5px);
        transition: font-size .2s ease .2s, transform .2s ease .2s;
        vertical-align: middle;
        font-size: 22px;
    }
	/*.db_login {
		font-size: 16px;
	}
	.db_login .db_login_top{
		position: relative;
		height: 50px;
		line-height: 50px;
		text-align: center;
		color: #333;
		font-weight: 600;
		border-bottom: 1px solid #f0f0f0;
	}
	.db_login .db_login_top .cancel{
		position: absolute;
		top: 0;
		left: 0;
		display: block;
		padding: 0 20px;
		color: #42bd56;
		font-size: 14px;
		font-weight: normal;
	}
	.db_login .db_login_form{
		padding: 0 15px;
		margin: 25px 0 5px;
	}
	.db_login .db_login_form .form_item{
		height: 45px;
		line-height: 45px;
		padding: 0 10px;
		margin-bottom: -1px;
		box-sizing: border-box;
		border: 1px solid #e0e0e0;
	}
	.db_login .form_item:nth-of-type(1){
		border-top-left-radius: 3px;
		border-top-right-radius: 3px;
	}
	.db_login .form_item:nth-of-type(2){
		border-bottom-left-radius: 3px;
		border-bottom-right-radius: 3px;
	}
	.db_login .db_login_form input{
		border: none;
	}
	.db_login .db_login_form .form_btn{
		margin-top: 10px;
	}
	.db_login .form_btn button{
		-webkit-appearance: none;
		-moz-appearance: none;
		appearance: none;
		border: 0;
		width: 100%;
		height: 40px;
		line-height: 40px;
		text-align: center;
		color: #fff;
		font-size: 14px;
		background-color: #17AA52;
		border-radius: 3px;
	}
	.db_login .login_other{
		color: #9d9d9d;
		text-align: center;
		margin-top: 15px;
	}
	.db_login .regist_download{
		text-align: center;
		margin-top: 40px;
	}
	.db_login .regist_download a{
		color: #42bd56;
		font-size: 14px;
		margin: 0 10px;
	}*/
</style>