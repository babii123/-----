<template>
  <div>
    <el-row>
      <el-col :span="12">
        <span
          style="
            margin: 1.5vw 0 0 1vw;
            font-size: x-large;
            font-weight: bold;
            display: flex;
            align-items: center;
          "
        >健康数据</span>
      </el-col>
      <el-col :span="12">
        <div style="float: right; position: relative">
          <el-date-picker
            v-model="pick_date"
            value-format="yyyy-MM-dd"
            style="position: absolute; transform: translate(-110%, 50%)"
            placeholder="今天"
          />
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-card style="width: 98%; margin: 1% auto 0 auto">
        <div style="text-align:center">
          <div class="circleBox_big">
            <el-progress
              :show-text="false"
              type="circle"
              :percentage="health_grade"
              :color="health_grade_color"
              :stroke-width="20"
              width="250"
            />
            <div class="circleCenter"><div style="font-size:100px">{{ health_grade }}</div><div style="font-size:20px">健康状态</div></div>
          </div>
          <!-- <el-image style="width: 25%" :src="require('./JS002.png')" /> -->
          <el-divider direction="vertical" />
          <div class="circleBox">
            <el-progress
              type="circle"
              :percentage="21.6"
              :color="health_grade_color"
              :stroke-width="10"
              width="120"
            />
            <div>JS错误</div>
          </div>
          <div class="circleBox">
            <el-progress
              type="circle"
              :percentage="14.5"
              :color="health_grade_color"
              :stroke-width="10"
              width="120"
            />
            <div>自定义异常</div>
          </div>
          <div class="circleBox">
            <el-progress
              type="circle"
              :percentage="10.7"
              :color="health_grade_color"
              :stroke-width="10"
              width="120"
            />
            <div>静态资源异常</div>
          </div>
          <div class="circleBox">
            <el-progress
              type="circle"
              :percentage="14.5"
              :color="health_grade_color"
              :stroke-width="10"
              width="120"
            />
            <div>接口异常</div>
          </div>
        <!-- <el-image style="width: 70%" :src="require('./JS003.png')" /> -->
        </div>
      </el-card>
    </el-row>
    <el-row style="margin: auto 0.5%">
      <el-col :span="6">
        <el-card style="margin: 2vw 0.5vw 0 0.5vw" display="inline">
          <div>
            <div>JS报错趋势 ></div>
            <div style="font-size: 10px">{{ pick_date }}</div>
            <JSerror />
          </div>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card style="margin: 2vw 0.5vw 0 0.5vw" display="inline">
          <div>
            <div>接口请求报错 ></div>
            <div style="font-size: 10px">{{ pick_date }}</div>
            <APIerror />
          </div>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card style="margin: 2vw 0.5vw 0 0.5vw" :inline="true">
          <div>
            <div>自定义异常趋势 ></div>
            <div style="font-size: 10px">{{ pick_date }}</div>
            <Customerror />
          </div>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card style="margin: 2vw 0.5vw 0 0.5vw" :inline="true">
          <div>
            <div>静态资源加载报错 ></div>
            <div style="font-size: 10px">{{ pick_date }}</div>
            <Assetserror />
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import JSerror from './components/JS_error.vue'
import APIerror from './components/API_error.vue'
import Customerror from './components/Custom_error'
import Assetserror from './components/Assets_error.vue'
// import request from '@/utils/request'

export default {
  components: {
    JSerror,
    APIerror,
    Customerror,
    Assetserror
  },
  data: function() {
    return {
      pick_date: '',
      health_grade: 86,
      health_grade_color: 'YellowGreen'
    }
  },
  mounted() {
    var date = new Date()
    var year = date.getFullYear()
    var month =
      date.getMonth() + 1 < 10
        ? '0' + (date.getMonth() + 1)
        : date.getMonth() + 1
    var day = date.getDate() < 10 ? '0' + date.getDate() : date.getDate()
    this.pick_date = year + '-' + month + '-' + day
    // console.log(this.pick_date)
  },

  methods: {
    // fetch_js_error(date){
    //   axios.post(
    //     '/jserror/counts',
    //     {
    //       date:date
    //     }
    //   ).then((res) =>{
    //     console.log("000000000000000000000")
    //     console.log(res)
    //   })
    // },
  }
}
</script>

<style scoped>
.el-divider--vertical {
  height: 13em;
  margin-top: -11%;
}
.main_container {
  width: 350px;
  height: 250px;
  overflow: hidden;
}
.circleBox_big{
  position: relative;
  text-align: center;
  margin: 1% 0 0 0;
  width: 20%;
  display: inline-block;
}
.circleBox{
  position: relative;
  text-align: center;
  margin: 0 0 0 0;
  width: 15%;
  display: inline-block;

}
.circleCenter{
  position: absolute;
  top:25%;
  left:33%;
}
</style>
