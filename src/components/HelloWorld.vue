<template>
  <div class="hello">
    <full-calendar
     :events="fcEvents"
     @eventClick="eventClick" 
     locale="en">
     </full-calendar>

  <div id="tem">
    <div  class="tooltip" role="tooltip" >
      <div class="tooltip-inner"></div>
  </div>
  </div>


  <div id="poper">
      <p v-for="k in cur_lines">
        {{k}}
      </p>
  </div>

  </div>
</template>

<script>
import fullCalendar from 'vue-fullcalendar'
import Tooltip from 'tooltip.js';



var demoEvents = [
	{
      title : 'lizn事件',
      start : '2019-06-1',
      end : '2019-06-04',
      msgs:[
        "2eqe",
        "sdfsdf"
      ],
  },
	{
      title : 'lizn事件',
      start : '2019-06-04',
      end : '2019-06-05'
  },
  	{
      title : 'lizn事件',
      start : '2019-06-07',
      end : '2019-06-09'
  },
   
]

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      fcEvents : demoEvents,
      cur_lines:{}
    }
  },
  components:{fullCalendar},
  methods:{
    
    eventClick: function(info,event) {


      var ss = document.getElementById('poper');
      var tem = document.getElementById('tem');

      var cur = this.fcEvents[info.cellIndex-1];

      this.cur_lines = cur.msgs

          console.log(cur);

      var tooltip = new Tooltip(event.target,
       {
      template: tem.innerHTML,
      title:ss,
      html:true,
      placement: 'top',
      trigger: 'blur',
      // container: 'body',
      boundariesElement:'',
      closeOnClickOutside:true,
      },
    );
    // vue的这个插件不支持 eventRender方法 所有不能在在
    //渲染过程中初始化，只能通过主动过调用show()方法来展示
    // 这样重复点击这个日历事件会引发bug

    // 方案1：自己改写 fullCalendar 使其支持 evenetRender 
      tooltip.show()



  }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
