<template>
    <div class="tab">
        <div class="tab-title">
            <ul>
                <li id="QRcode-title" 
                    v-for="(item, index) in title"
                    v-bind:key="index">{{item}}</li>
            </ul>
        </div>
        <div class="tab-content">
            <div id="QRcode-tab" hidden >
                <input placeholder="请输入用户名"/>
                <input placeholder="请输入验证码"/>
            </div>
            <div id="verificationCode-tab" hidden>
                二维码
            </div>
        </div>            
    </div>
</template>

<script>
export default {
    data(){
        return{
            title:['二维码', '验证码']
        }
    }
}
</script>


<style>
.tab {
    width: 100%;
    height: 100%;
}

.tab li:hover{
    border:1px solid #CC1A0D;
    cursor: pointer;
}

.tab ul {
    width: 100%;
    display: flex;
}

.tab li {
    width: 50%;
    height: 30px;
    line-height: 30px;
    text-align: center;
    border: 1px solid #999;
}

.tab .active-title{
    background-color: #ED928B;
    color: #ffffff;
}

.tab .active-content{
    display: block;
}
</style>

