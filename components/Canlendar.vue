<template>
    <div class="canlendar">
        <div class="canlendar-top">
            <div class="icon-round" @click="subYear"> &lt;&lt; </div>
            <div class="icon-round" @click="subMonth"> &lt; </div>
            <div>{{selectedYear}}年{{selectedMonth}}月{{selectedDay}}日</div>
            <div class="icon-round" @click="addMonth"> &gt; </div>
            <div class="icon-round" @click="addYear"> &gt;&gt; </div>
        </div>
        <div class="canlendar-body">
            <table>
                <thead>
                    <tr>
                        <th>日</th>
                        <th>一</th>
                        <th>二</th>
                        <th>三</th>
                        <th>四</th>
                        <th>五</th>
                        <th>六</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="i in weeks"
                        v-bind:key="i">
                        <td v-for=" d in 7"
                            v-bind:key = "d"
                           >{{ ((i-1)*7+d- firstDay)>=1 ? (i-1)*7+d- firstDay > selectedAllDays ? '' :(i-1)*7+d- firstDay:'' }}</td>
                        </tr>
                </tbody>
            </table>
        </div>
        <div class="canlendar-bottom">
        </div>

    </div>
</template>

<script>
export default {
    data(){
        return{
            selectedYear:'',
            selectedMonth:'',
            selectedDay:'',
        }
        
    },
    methods:{
        subYear:function () { 
            this.selectedYear = this.selectedYear - 1 
            },
        subMonth:function () { 
            if(this.selectedMonth === 1){
                this.selectedMonth = 12;
                this.selectedYear = this.selectedYear-1
            } else {
                this.selectedMonth = this.selectedMonth - 1
                }
                },
        addYear:function () { 
            this.selectedYear = this.selectedYear + 1 
            },
        addMonth:function () { 
            if(this.selectedMonth === 12){
                this.selectedMonth = 1;
                this.selectedYear = this.selectedYear + 1;
            } else {this.selectedMonth = this.selectedMonth + 1 } },

    },
    created:function () {
    var currDate = new Date(); //当前时间

    this.selectedYear = currDate.getFullYear(); // 获取当前年
    this.selectedMonth = currDate.getMonth() + 1; // 获取当前月
    this.selectedDay = currDate.getDate(); //获取当前日

    },

    computed:{
        // 获取当前月份的总天数
        selectedAllDays:function () {
            var twelveMonths = []; 
                //判断当前年是不是闰年
            if( this.selectedYear % 400 === 0 || (this.selectedYear % 4 === 0 && this.selectedYear % 100 != 0 )){
                twelveMonths = [31,28,31,30,31,30,31,31,30,31,30,31]
            } else {
                twelveMonths = [31,29,31,30,31,30,31,31,30,31,30,31]
            };
             
            return twelveMonths[this.selectedMonth-1];
          },

        firstDay:function () { 
            // 判断当前月的1号是星期几
            var currMonthFirstDay = new Date(this.selectedYear, this.selectedMonth-1, 1);
            return currMonthFirstDay.getDay();
          },
        
        weeks:function(){
            return Math.ceil((this.selectedAllDays + this.firstDay)/7);
        }
    }
    
}
</script>


<style scoped>
.canlendar{
    width: 100%;
    height: 100%;
    border-radius: 12px;
}
.canlendar-top
{
    height: 10%;
    border: 1px solid #999;
    display: flex;
    justify-content:space-around;
    align-items: center;
    border-radius: 12px 12px 0 0;
}
.canlendar-body
{
    height: 80%;
}
.canlendar-bottom
{
    height: 10%;
}

.canlendar-body table{
    width: 100%;
    border-collapse: collapse;
}

.canlendar-body table tr,th,td{ 
    border: 1px solid #999;
    height: 36px;
    text-align: center;
    line-height: 36px;
}

.canlendar-top .icon-round{
    width: 30px;
    height: 30px;
    text-align: center;
    line-height: 30px;
}

.canlendar-top .icon-round:hover{
    width: 30px;
    height: 30px;
    text-align: center;
    line-height: 30px;
    border-radius: 15px;
    background-color: #ef8b70;
    color: #ffffff;
    cursor: pointer;
}

.canlendar-body table td:hover{
    background-color: #ef8b70;
    color: #ffffff;
    cursor: pointer;
}

</style>

