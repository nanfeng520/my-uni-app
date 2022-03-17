<template>
  <div class="my-prize">
    <div class="prize-content">
      <div class="prize-title">恭喜您，已领取一级任务奖品</div>
      <div class="prize-describe">长按识别二维码，添加客服领取奖品</div>
      <div class="gift-box">
          <div class="gift-box-c">
            <img src="./images/code.png" alt="">
          </div>
      </div>
      <div class="prize-base">
          <img src="./images/prize-base.png" alt="">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyPrize'
}
</script>

<style scoped lang='scss'>
@import "~@/assets/css/style/mixin.scss";
.my-prize {
  height: 100%;
  width: 100%;
  background: url('./images/prize-back.png') no-repeat;
  background-size: 100% 100%;
  padding: px2rem(160) px2rem(50) px2rem(156) px2rem(50);
  box-sizing: border-box;
  .prize-content {
    height: 100%;
    width: 100%;
    background: linear-gradient(360deg, #FAFAFA 0%, #FFFFFF 21%, #F0F2F4 26%, #EDEFF2 29%, #F4F4F6 64%, #FCFCFC 100%);
    box-shadow: 0px px2rem(8) px2rem(40) px2rem(2) rgba(205,205,205,0.35);
    border-radius: px2rem(8);
    padding: px2rem(80) px2rem(48) px2rem(62) px2rem(48);
    box-sizing: border-box;
    .prize-title {
      margin-bottom: px2rem(16);
      font-weight: 500;
      color: #595959;
      font-size: px2rem(36);
    }
    .prize-describe {
      font-size: px2rem(24);
      color: #595959;
      margin-bottom: px2rem(96);
    }
    .prize-base {
      margin: 0px auto;
      margin-top: px2rem(-55);
      text-align: center;
      // width: px2rem(513);
      // height: px2rem(262);
    }
    .gift-box {
      position: relative;
      width:px2rem(470);
      height: px2rem(588);
      margin: 0px auto;
      .gift-box-c {
        // position: absolute;
        top: 0;
        left: 0;
        width:100%;
        height: 100%;
        background: url('./images/gift-box.png') no-repeat;
        background-size: 100% 100%;
        margin: 0px auto;
        text-align: center;
        & > img {
            width: px2rem(340);
            height: px2rem(340);
            margin-top: px2rem(27);
            border-radius: px2rem(20);
        }
     }
    }

  }
}
</style>
