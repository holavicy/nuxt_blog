<template>
<section class="login">
    <div>
        <top/>
    </div>
    <div>
        <div style="display:flex;">
            <div class="login-content-left">
                <div class="login-content-left-canlendar">
                   <canlendar />
                </div>
                <div class="login-content-left-text">
                    文本    
                </div>
            </div>
            <div class="login-content-right">
                <div class="login-content-right-form">
                    <div style="height:90%">
                        <tab />
                    </div>
                    <div style="display:flex; justify-content:center">
                        <nuxt-link to="/today/plane" >
                        <button class="nuxt_btn_base nuxt_btn_primary" style="width:100px">登录</button>
                    </nuxt-link>
                    </div>
                   
                </div>
            </div>
           
        </div>
       
    </div>
</section>
</template>

<script>
import Top from '~/components/Top.vue'
import Canlendar from '~/components/Canlendar.vue'
import Tab from '~/components/utils/Tab.vue'

export default {
    components: {
        Top,Canlendar,Tab
    },
}

</script>

<style scoped>
.login-content-left {
    width: 70%;
    height: 800px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.login-content-right {
    width: 30%;
    height: 800px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.login-content-left-canlendar{
    margin-top: 20px;
    width: 40%;
    height: 360px;
}
.login-content-left-text{
    width: 90%;
    height: 400px;
    margin-top: 10px;
    border: 1px solid #999;
    border-radius: 12px;
    box-shadow:2px 3px 5px #888888 
}
.login-content-right-form{
    width: 60%;
    height: 300px;
    border: 1px solid#eee;
    margin-top: 160px;
    padding: 10px;

}
</style>
