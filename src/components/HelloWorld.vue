<template>

    <main ref="wrapper" class="scroll_box">
      <div class="list" v-if="dataList.length">
        <div class="list_item" v-for="(item, index) of dataList" :key="index" @click="check(item)">
          <div class="img_wrap">
            <img :src="item.storeLogo" />
          </div>
          <div class="right_box">
            <div class="title">
              <div class="name">{{ item.storeName }}</div>
              <span :class="checkList.includes(item.orderSn) ? 'checked' : ''"></span>
            </div>
            <div class="rows">
              <div class="row">
                <span class="text_left">就餐人数</span>
                <span class="text_right">{{ item.mealNumber }}人</span>
              </div>
              <div class="row">
                <span class="text_left">就餐时间</span>
                <span class="text_right">{{ item.banquetAt }}</span>
              </div>
              <div class="row">
                <span class="text_left">联系信息</span>
                <span class="text_right">{{ item.contactName }} {{ item.contactPhone}}</span>
              </div>
            </div>
            <div class="pay_amount vux-1px-t">
              <div class="text_left">支付金额</div>
              <div class="text_right">&yen;{{ item.thirdPayAmount }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="bottom">
        <div class="left_box vux-1px-t">
          <div class="checkbox" @click="handleClick">
            <span class="check" :class="{ checked: isCheckAll }"></span>
            <span class="label">全选</span>
          </div>
          <div class="total">{{ checkList.length }}个订单，合计{{ totalAmount }}元</div>
        </div>
        <div class="submit">提交</div>
      </div>
    </main>
</template>

<script>
  export default {
    name: 'expense',
    data () {
      return {
        dataList: [
          {
            storeLogo: 'http://b-ssl.duitang.com/uploads/item/201805/13/20180513224039_tgfwu.png',
            orderSn: 1,
            mealNumber: 1,
            contactName: 'motys',
            contactPhone: '13888888888',
            thirdPayAmount: 12
          },
          {
            storeLogo: 'http://b-ssl.duitang.com/uploads/item/201805/13/20180513224039_tgfwu.png',
            orderSn: 2,
            mealNumber: 1,
            contactName: 'motys',
            contactPhone: '13888888888',
            thirdPayAmount: 12
          },
          {
            storeLogo: 'http://b-ssl.duitang.com/uploads/item/201805/13/20180513224039_tgfwu.png',
            orderSn: 3,
            mealNumber: 1,
            contactName: 'motys',
            contactPhone: '13888888888',
            thirdPayAmount: 12
          },
          {
            storeLogo: 'http://b-ssl.duitang.com/uploads/item/201805/13/20180513224039_tgfwu.png',
            orderSn: 4,
            mealNumber: 1,
            contactName: 'motys',
            contactPhone: '13888888888',
            thirdPayAmount: 12
          },
          {
            storeLogo: 'http://b-ssl.duitang.com/uploads/item/201805/13/20180513224039_tgfwu.png',
            orderSn: 5,
            mealNumber: 1,
            contactName: 'motys',
            contactPhone: '13888888888',
            thirdPayAmount: 12
          },
          {
            storeLogo: 'http://b-ssl.duitang.com/uploads/item/201805/13/20180513224039_tgfwu.png',
            orderSn: 5,
            mealNumber: 1,
            contactName: 'motys',
            contactPhone: '13888888888',
            thirdPayAmount: 12
          }
        ],
        checkList: [],
        totalList: [],
        ticket: ''
      }
    },
    computed: {
      // 判断是否全部选中
      isCheckAll () {
        if (this.checkList.length === this.dataList.length) {
          return true
        }
        return false
      },
      totalAmount () {
        let total = 0;
        if (this.checkList.length) {
          total = this.totalList.reduce((prev, cur) => {
            return prev + cur
          }, 0)
        }
        return total
      }
    },
    methods: {
      // 多选
      check (item) {
        let idx = this.checkList.indexOf(item.orderSn)
        // 如果是选中就取消选中，没有就选中
        if (idx > -1) {
          this.checkList.splice(idx, 1)
          this.totalList.splice(idx, 1)
        } else {
          this.checkList.push(item.orderSn)
          this.totalList.push(item.thirdPayAmount)
        }
      },
      // 选中全部
      checkAll () {
        this.checkList = []
        this.dataList.forEach((item) => {
          this.checkList.push(item.orderSn)
          this.totalList.push(item.thirdPayAmount)
        })
      },
      // 清空选择
      clearCheck () {
        this.checkList = []
        this.totalList = []
      },

      // 全选按钮
      handleClick () {
        // 如果是全选就清空选择，不是就选中全部
        if (this.isCheckAll) {
          this.clearCheck()
        } else {
          this.checkAll()
        }
      }
    }
  }
</script>

<style lang="less" scoped>
  .scroll_box {
    height: 100vh;
    position: relative;
    .list {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      overflow-y: auto;
      padding: 11px 10px;
      .list_item {
        display: flex;
        padding: 14px 8px 0 9px;
        background: #FFF;
        border-radius: 8px;
        & + .list_item {
          margin-top: 12px;
        }
        .img_wrap {
          margin-right: 14px;
          width: 44px;
          height: 44px;
          border-radius: 50%;
          overflow: hidden;
          img {
            width: 100%;
            height: 100%;
          }
        }
        .right_box {
          flex: 1;
          .title {
            height: 44px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            .name {
              width: 165px;
              white-space: nowrap;
              text-overflow: ellipsis;
              overflow: hidden;
              font-size: 15px;
              color: #333;
              font-weight: 500;
            }
            span {
              width: 14px;
              height: 14px;
              background: url(../assets/icon_check.png) no-repeat center/contain;
              &.checked {
                background: url(../assets/icon_checked.png) no-repeat center/contain;
              }
            }
          }
          .rows {
            margin-top: 19px;
            padding-right: 4px;
            .row {
              padding-bottom: 8px;
              display: flex;
              justify-content: space-between;
              .text_left {
                font-size: 12px;
                color: #999;
              }
              .text_right {
                font-size: 12px;
                color: #333;
              }
            }
          }
          .pay_amount {
            padding-right: 4px;
            height: 34px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #333;
            .text_left {
              font-size: 13px;
            }
            .text_right {
              font-size: 12px;
              font-weight: 500;
            }
          }
        }
      }
    }
    .bottom {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      display: flex;
      justify-content: space-between;
      height: 47px;
      background: #FFF;
      .left_box {
        flex: 1;
        padding-left: 10px;
        .checkbox {
          padding-top: 6px;
          width: 25%;
          height: 26px;
          font-size: 0;
          .check {
            margin-right: 3px;
            display: inline-block;
            width: 12px;
            height: 12px;
            vertical-align: sub;
            background: url(../assets/icon_check.png) no-repeat center/contain;
            &.checked {
              background: url(../assets/icon_checked.png) no-repeat center/contain;
            }
          }
          .label {
            font-size: 14px;
            color: #666;
          }
        }
        .total {
          font-size: 12px;
          color: #333;
          font-weight: 500;
        }
      }
      .submit {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 113px;
        background: #0398FF;
        font-size: 18px;
        color: #FFF;
        font-weight: 500;
      }
    }
  }

</style>
