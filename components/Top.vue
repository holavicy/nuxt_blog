<template>
    <div class="header_top">
        <nuxt-link to="/"> <img src="~/assets/images/nuxt.png" alt=""></nuxt-link>
        <div class="header_top_title">
            first_example
            <span class="header_top_desc">基于nuxt的个人blog系统</span>
        </div> 
        <div class="header_top_user">
            <img src="~/assets/images/user-red-32px.png" alt="">
        </div> 
        <div class="header_top_user_options">
            <ul>
                <li>1</li>
                <li>2</li>
                <li>3</li>
                <li>4</li>
            </ul>
        </div>
        
    </div>
</template>

<script>

export default {
    methods: {
        homePage: function(){
            alert("返回首页")
        }
    }
}
</script>


<style>
.header_top{
    width: 100%;
    border-bottom: 1px solid #aaaaaa;
    display: flex;
    justify-content:center;
}

.header_top_title{
    margin: 0 auto;
    height: 50px;
    line-height: 50px;
    font-size: 2rem;
}

.header_top_desc{
    color: #cecece;
    font-size: 0.8rem;
}

.header_top_user{
    padding:9px 0; 
    margin-right:20px;
    position: relative;
}

.header_top_user_options{
    position: absolute;
    top:50px;
    right: 23px;
}

.header_top_user_options ul{
    padding: 0;
    margin: 0;
    list-style: none;
    width: 32px;
    border: 1px solid #bf4231;
    border-top: 0;
    border-radius: 12px 12px 0 0 ;
}

.header_top_user_options ul li{
    padding: 0;
    margin: 0;
    width: 100%;
    border-bottom: 1px solid #bf4231;
    color: #bf4231;
    text-align: center;
    cursor: pointer;
}
</style>
