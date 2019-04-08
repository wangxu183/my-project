<template>
  <div>
    <i-notice-bar icon="systemprompt" loop>
      {{notice}}脚步到不了的地方，文字可以！！
    </i-notice-bar>
     <i-grid i-class="no-border">
       <i-grid-item v-for="item in grids" :key="item" i-class="no-border">
          <i-grid-label>{{item}}</i-grid-label>
       </i-grid-item>
    </i-grid>
    <i-grid i-class="no-border">                                                                                                                                                                                                    
      <i-grid-item i-class="no-border">
        <i-grid-icon>
            <image src="/static/tabs/1.png" />
        </i-grid-icon>
        <i-grid-label>点心</i-grid-label>
      </i-grid-item >  
      <i-grid-item i-class="no-border">
        <i-grid-icon>
            <image src="/static/tabs/2.png" />
        </i-grid-icon>
        <i-grid-label>主食</i-grid-label>
      </i-grid-item>
      <i-grid-item i-class="no-border">
        <i-grid-icon>
            <image src="/static/tabs/3.png" />
        </i-grid-icon>
        <i-grid-label>外卖</i-grid-label>
      </i-grid-item>
     </i-grid>
     <i-grid i-class="no-border">
      <i-grid-item i-class="no-border">
        <i-grid-icon>
            <image src="/static/tabs/4.png" />
        </i-grid-icon>
        <i-grid-label>饮料</i-grid-label>
      </i-grid-item>  
      <i-grid-item i-class="no-border">
        <i-grid-icon>
            <image src="/static/tabs/5.png" />
        </i-grid-icon>
        <i-grid-label>菜蔬</i-grid-label>
      </i-grid-item>
      <i-grid-item i-class="no-border">
        <i-grid-icon>
            <image src="/static/tabs/6.png" />
        </i-grid-icon>
        <i-grid-label>面食</i-grid-label>
      </i-grid-item>
    </i-grid>
    <i-panel title="美食推荐">

      <view v-for="item in candys" :key="item" class="top-padding">
         <i-card  :title="item.name" :extra="item.introduction" thumb="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554136734498&di=4a94d72ac1a61ec76e83c1e5e6202629&imgtype=0&src=http%3A%2F%2Fimg1.qunarzz.com%2Fp%2Ftts6%2F1702%2Fa4%2Feac2c8a1e491e02.jpg_r_750x500x90_d537b527.jpg">
          <view slot="content">{{item.type}}</view>
          <view slot="footer">{{item.commitment}}</view>
         </i-card>
      </view>
         <!-- <view class="top-padding"></view>
         <i-card title="马卡龙" extra="超级好吃" thumb="http://img1.imgtn.bdimg.com/it/u=2023513984,2730774655&fm=26&gp=0.jpg">
          <view slot="content">超级好看呢</view>
          <view slot="footer">一款超级好看还超级好吃的甜品</view>
         </i-card>
         <view class="top-padding"></view>
         <i-card title="榴莲" extra="水果之王" thumb="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554137156969&di=d23f99f8475cabbabd7fb777c4b18413&imgtype=0&src=http%3A%2F%2Fbmp.skxox.com%2F201607%2F16%2Fbanghong520.112723.jpg">
          <view slot="content">超级好吃，还美容</view>
          <view slot="footer">就是脂肪含量很高，易发胖，不易吃多</view>
         </i-card>
        <view class="top-padding"></view>
         <i-card title="辣条" extra="就是挺喜欢吃的" thumb="http://img2.imgtn.bdimg.com/it/u=1535460409,2183749429&fm=26&gp=0.jpg">
          <view slot="content">辣条这个。。这个。。哈哈哈</view>
          <view slot="footer">最然喜欢吃，但是还是要少吃，毕竟不健康</view>
         </i-card>  -->
         <!-- <view class="top-padding"></view> -->
    
    </i-panel>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      candys: [],
      notice: '有人说：',
      grids: ['点心','主食','外卖','饮料','菜蔬','面食'],
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      }
    }
  },

  components: {
    card
  },

  created () {
    const db = wx.cloud.database({ env:'wangxu-44b924' })
    db.collection('candy').get().then(
      res => {
        console.log(res)
        this.candys = res.data
      }
    )
  },


  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped>
div >>> .no-border{
  border-width:  0pt;
}
div >>> .top-padding{
  padding-top:50rpx;
}

.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all{
  width:7.5rem;
  height:1rem;
  background-color:blue;
}
.all:after{
  display:block;
  content:'';
  clear:both;
}
.left{
  float:left;
  width:3rem;
  height:1rem;
  background-color:red;
}

.right{
  float:left;
  width:4.5rem;
  height:1rem;
  background-color:green;
}
</style>
