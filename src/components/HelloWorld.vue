<template lang="html">
  <div>
    <img src="../assets/bg.png" alt="" class="bg">
    <div class="content">
      <div class="content-middle">
        <div class="middle-title">
          实时提现记录
        </div>
        <div class="fg">
          <ul class="fg-content">
            <li class="middle-item" v-for="item in dataList">
              <div class="table-cell">
                <img class="avater" :src="item.avatar" alt="">
              </div>
              <div class="table-cell-2">
                <span class="username">{{item.nick_name}}</span>
                <span class="updateTime">1分钟前</span>
              </div>
              <div class="money">
                <span>{{item.item_name}}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      dataList: []
    }
  },
  created() {
    this._getData()
  },
  methods: {
    _getData() {
      axios.get('/api/data').then((res) => {
        var sortdata = this.randomSort(res.data.data)
        this.dataList = sortdata
      })
    },
    randomSort(arr) {
      var array = arr.slice();
      array.sort(function() {
        return 0.5 - Math.random()
      })
      return array
    }
  }
}
$(function(){
  $('.bg').on('click',function(){
    console.log(1)
  })

  var height = $('.fg-content li').height()
  function hanshu(){
		$(".fg-content").animate({"top": - height + 'px' },function(){
			$(".fg-content .middle-item:eq(0)").appendTo($(".fg-content"))
			$(".fg-content").css({"top":0})
		})
	}
	var jinjin = setInterval(hanshu,1000)
})
</script>

<style lang="stylus">
  .bg
    width 100%;
  .content
    width 100%;
    .content-middle
      width: 95%;
      height: 11rem;
      background: #ffb300;
      margin: 0px auto;
      margin-bottom: 1rem;
      border-radius:10px;
      overflow:hidden;
      .middle-title
        width: 95%;
        height: 1rem;
        text-align: center;
        line-height: 1rem;
        font-size: 0.7rem;
        color: #fff;
        border-bottom: 1px solid #fff;
        font-weight: bold;
        margin: 0px auto;
      .fg
        width:95%;
        height:10rem;
        margin:0px auto;
        overflow:hidden;
        position:relative;
        ul
          position:absolute;
          width:100%;
          li
            height:2rem;
            border-bottom:1px solid #ffffff;
            display:flex;
            .table-cell
              height: 2rem;
              display: flex;
              width: 1.5rem;
              .avater
                width:1.5rem;
                height:1.5rem;
                border-radius:50%;
                margin:auto;
            .table-cell-2
              display:flex;
              width:3rem;
              flex-direction:column;
              .username
                font-size: 0.3rem;
                width: 90%;
                height: 1rem;
                color: #fff;
                line-height: 1.3rem;
                font-weight: bold;
                margin-left: 10px;
              .updateTime
                font-size: 0.3rem;
                width: 90%;
                height: 1rem;
                color: #fff;
                line-height: 0.6rem;
                margin-left: 10px;
            .money
              display:flex;
              width:3rem;
              span
                font-size: 0.3rem;
                color: #fff;
                margin-left: 0.65rem;
                line-height: 2rem;



</style>
