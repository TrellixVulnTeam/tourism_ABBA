<template>
  <div>
    <top></top>
    <div class="cotainer teamInfor">
      <div class="f1">
        <div>
          <el-carousel trigger="click" height="150px">
            <el-carousel-item v-for="item in teamInfor.fileList" :key="item">
              <div
                class="img"
                :style="{ background: 'url(' + item + ')' }"
              ></div>
            </el-carousel-item>
          </el-carousel>
        </div>

        <div class="f1_right">
          <h3>{{ teamInfor.introduce }}</h3>
          <div>
            <span>{{ teamInfor.departure }}</span>
            >>>>
            <span>{{ teamInfor.destination }}</span>
          </div>
          <div class="price">
            <h3>￥{{ teamInfor.price }}</h3>
            <el-button type="success" @click="open">预定名额</el-button>
          </div>
        </div>
      </div>
      <hr />
      <div class="f2">
        <div>
          <h2>行程安排</h2>
          <el-timeline>
            <el-timeline-item
              v-for="(item, index) in teamInfor.buZhou"
              :key="index"
              placement="top"
            >
              <el-card>
                <h4>{{ item }}</h4>
              </el-card>
            </el-timeline-item>
            <div class="arcle">文章Id:{{ this.teamInfor.tId }}</div>
          </el-timeline>
        </div>
        <div>
          提供商：{{ teamInfor.provider }}
          <div>
            温馨提示
            <br />
            【关于购物场所】
            1.在旅游行程中，个别景点景区、餐厅、休息区等场所存在商场等购物场所，上述场所非旅行社安排的指定购物场所。本公司提醒旅游者根据自身需要，理性消费并索要必要票据。如产生消费争议，请自行承担相关责任义务，由此带来的不便，敬请谅解！
            2.目的地可能有部分私人经营的娱乐、消费场所，此类组织多数无合法经营资质，存在各种隐患。为了您的安全和健康考虑，本公司提醒您，谨慎消费；
            <br />
            【关于不可抗力因素】
            1.本产品行程实际出行中，导游、司机可能会根据天气、交通等情况，对您的行程进行适当调整（如调整景点游览顺序等），以确保行程顺利进行。如因不可抗力等因素确实无法执行原行程计划，对于因此而造成的费用变更，我社实行多退少补，敬请配合；
            2.行程中的赠送项目，如因交通、天气等不可抗因素导致不能赠送的、或因您个人原因不能参观的，费用不退，敬请谅解；
            3.因玉龙雪山冰川大索道实行限票制，旺季（暑假、寒假、春节等节假日）期间出行不保证上大索道，如实际出行时上不了大索道则退门票差价安排小索道，望知晓。
            4.如遇春节、元旦、国庆、寒暑假等旺季出行，动车票资源紧张，本社会调整火车卧铺或汽车往返，请知晓！
            5.如遇春节、元旦、国庆、寒暑假等旺季出行，国际五星酒店因资源紧张无法安排，则安排至同级酒店或退差价安排商务酒店。
            <br />
            【温馨提示】
            1.全程请您妥善保管好您的身份证件及贵重物品，以免因遗失等情况影响了旅行；
            2.由于旅游产品包含因素较多，为提高客户体验，我社会对产品进行更新、升级；您拍下付款时的产品细节和您出行的产品细节会有所出入，在您抵达昆明时，我社工作人员会把准确的行程单与您核对，行程将按照行程单执行。
            3.此行程为特价打包产品，指定最少2成人及以上预定，低于此人数下单视为无效订单，不便之处，敬请谅解！
            4.因客人是失信人员导致乘坐不了飞机、火车、高铁，并未提前告知工作人员，所产生的一切费用自行承担。
            5.8人及以上出游人数下单前请先咨询客服！如果未咨询拍下付款，则视为无效订单，不便之处，敬请谅解！
            6.本行程只支持纸质版合同，会在抵达昆明的第一天由合同专员当面签署并讲解行程及注意事项，请知晓！
            7.由于铁路局政策原因，如客人由于自身原因需火车/动车退票、改期，请持身份证原件自行操作，望悉知！
            8.跟团产品需您全程跟团，期间不可出现离团及脱团行为，请您予以配合。如您擅自离团，视为您单方面违约，需承担已损失的机票、车费、住宿费，旅行社有权在您违约后终止您的后继行程及服务，包括您的回程机票，之后发生的任何事情均需您自行全权负责。
            9.该团为各地游客散拼组成，出发地不同，机票价格不一致会导致所拍价格不一致，行程段具体以合同为准，望悉知！
          </div>
        </div>
        <div></div>
      </div>
    </div>
  </div>
</template>

<script>
import top from "@/components/Top/page";
export default {
  components: {
    top,
  },
  data() {
    return {
      teamInfor: {},
    };
  },
  methods: {
    open() {
      this.$prompt("请输入电话号", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        inputPattern: /^[1]([3-9])[0-9]{9}$/,
        inputErrorMessage: "格式不正确",
      })
        .then(({ value }) => {
          this.axios
            .post(this.$root.team + "savePhoneNum/" + value)
            .then((res) => {
              if (res.data) {
                this.$message({
                  type: "success",
                  message: "提交成功" + value,
                });
              }
            })
            .catch((err) => {
              console.error(err);
            });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "取消输入",
          });
        });
    },
  },
  mounted() {
    this.teamInfor = JSON.parse(this.$route.query.item);
  },
};
</script>

<style scoped>
.teamInfor {
  padding: 20px;
}
.f1 {
  display: flex;
}
.f1 > div:nth-child(1) {
  width: 30%;
}
.f1 > div:nth-child(2) {
  width: 60%;
  margin-left: 10%;
}
.el-carousel__item .img {
  width: 100%;
  height: 100%;
  background-position: center !important;
  background-size: contain !important;
  background-repeat: no-repeat !important;
}
.f2 > div:nth-child(2) {
  width: 40%;
  max-width: 40%;
}
.f1_right > div:nth-child(2) > span {
  color: orange;
}
.price {
  color: orangered;
  display: flex;
  align-items: center;
}
.f2 {
  display: flex;
}
.f2 > div:nth-child(1) {
  width: 60%;
  border-right: dashed 1px black;
  padding: 20px;
}
.price > button {
  margin-left: 40px;
}
.f2 > div:nth-child(2) {
  padding: 20px;
}
.arcle {
  font-size: 10px;
  color: grey;
  margin-top: 10px;
}
</style>