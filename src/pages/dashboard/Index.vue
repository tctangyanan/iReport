<template>
  <div class="dashboard-page">
    <!--region 栏目-->
    <el-row class="panel-group" :gutter="40">
      <template v-for="(panel, index) in panelList">
        <el-col :key="index" :xs="12" :sm="12" :lg="6" class="card-panel-col">
          <div class='card-panel' @click="handleSetLineChartData(panel.id)">
            <div class="card-panel-icon-wrapper icon-people">
              <div :class="`card-panel-icon panel-${panel.color}`">
                <span class="axon-icon" v-html="panel.icon"></span>
              </div>
            </div>
            <div class="card-panel-description">
              <div class="card-panel-text">{{ panel.label }}</div>
              <count-to class="card-panel-num" :startVal="0" :endVal="panel.value" :decimals=2 :duration="2600"></count-to>
            </div>
          </div>
        </el-col>
      </template>
    </el-row>
    <!--endregion-->
    <!--region 创建新场景-->
    <div class="add-new-scene">
      <el-button type="primary" icon="el-icon-plus" plain round @click.native="creatNewScene">添加新场景</el-button>
    </div>
    <!--endregion-->
  </div>
</template>
<script>
const CountTo = () => import('vue-count-to')
const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}
export default {
  components: { CountTo },
  data () {
    return {
      panelList: [
        {
          id: 'newVisitis',
          label: 'Demo1',
          value: 102400,
          icon: '&#xe63e;',
          color: 1// '#40c9c6'
        },
        {
          id: 'messages',
          label: 'Demo2',
          value: 81212,
          icon: '&#xe72d;',
          color: 2 // '#36a3f7'
        },
        {
          id: 'purchases',
          label: 'Demo3',
          value: 9280.3,
          icon: '&#xe736;',
          color: 3 // '#f4516c'
        },
        {
          id: 'shoppings',
          label: 'Demo4',
          value: 13600.6,
          icon: '&#xe61b;',
          color: 4 // '#34bfa3'
        }
      ],
      lineChartData: lineChartData.newVisitis
    }
  },
  mounted () {
  },
  methods: {
    handleSetLineChartData (panel) {
      this.lineChartData = lineChartData[panel]
    },
    /**
     * 创建新场景
     */
    creatNewScene () {
      this.$router.push({ path: '/editor' })
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../../styles/font.scss";

.dashboard-page {
  background-color: #f0f2f5;
  padding: 32px;
  overflow-y: auto;
  .panel-group {
    padding: 40px 0;
    .card-panel-col {
      margin-top: 10px;
      .card-panel {
        height: 108px;
        cursor: pointer;
        font-size: $font-size-s;
        position: relative;
        overflow: hidden;
        color: #666;
        background: #fff;
        -webkit-box-shadow: 4px 4px 40px rgba(0, 0, 0, 0.05);
        box-shadow: 4px 4px 40px rgba(0, 0, 0, 0.05);
        border-color: rgba(0, 0, 0, 0.05);
        display: flex;
        padding: 0 20px;

        &:hover {
          .card-panel-icon-wrapper {
            .card-panel-icon {
              border-radius: 4px;
              transition: all 0.38s ease-out;
              &.panel-1 {
                background-color: #40c9c6;
                .axon-icon {
                  color: #ffffff;
                }
              }
              &.panel-2 {
                background-color: #36a3f7;
                .axon-icon {
                  color: #ffffff;
                }
              }
              &.panel-3 {
                background-color: #f4516c;
                .axon-icon {
                  color: #ffffff;
                }
              }
              &.panel-4 {
                background-color: #34bfa3;
                .axon-icon {
                  color: #ffffff;
                }
              }
            }
          }
        }
        .card-panel-icon-wrapper {
          flex: 0 0 50%;
          .card-panel-icon {
            width: 60px;
            height: 60px;
            margin-top: 29px;
            text-align: center;
            line-height: 60px;
            &.panel-1 {
              .axon-icon {
                color: #40c9c6;
              }
            }
            &.panel-2 {
              .axon-icon {
                color: #36a3f7;
              }
            }
            &.panel-3 {
              .axon-icon {
                color: #f4516c;
              }
            }
            &.panel-4 {
              .axon-icon {
                color: #34bfa3;
              }
            }
            .axon-icon {
              font-size: $font-size-large;
            }
          }
        }
        .card-panel-description {
          flex: 0 0 50%;
          text-align: right;
          margin: 26px 0;
          .card-panel-text {
            font-size: $font-size-xxl;
            font-weight: 600;
            line-height: 32px;
            color: rgba(0, 0, 0, 0.45);
          }
          .card-panel-num {
            font-weight: 600;
            font-size: $font-size-xxxl;
          }
        }
      }
    }
  }
  .add-new-scene {
    text-align: center;
  }
}
</style>
