<template>
  <div>
    <el-tabs v-model="activeName" @tab-click="moduleSwitch">
      <!-- name属性对应着 栏目ID，通过它查找 内容 -->
      <el-tab-pane label="搭配" name="9441">
        <!-- 轮播图与精彩瞬间、学生风采同属一个组件 -->
        <!-- <tableWithImg
          :projects="projects9441"
          :categoryId="9441"
          @showClicked="shownHandler($event)"
          @deleteClicked="deleteHandler($event)"
          @updateClicked="updateHandler($event)"
        ></tableWithImg> -->
        <el-table
    :data="tableData"
    stripe
    style="width: 100%">
    <el-table-column
      prop="date"
      label="编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="搭配"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="优劣">
    </el-table-column>
  </el-table>
  <el-pagination
  background
  layout="prev, pager, next"
  :total="100">
</el-pagination>
      </el-tab-pane>
      <el-tab-pane label="功效结果" name="9411">
        <el-table
    :data="tableDatas"
    stripe
    style="width: 100%">
    <el-table-column
      prop="date"
      label="编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="优劣"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="功效与劣势">
    </el-table-column>
  </el-table>
      </el-tab-pane>
      <el-tab-pane label="常见问题" name="9440">
        <!-- 常见问题与游学项目同属一个组件 -->
        <simpleTable
          :projects="projects9440"
          :categoryId="9440"
          :labelArr="[
            { label: '姓名', prop: 'name' },
            { label: '回答内容', prop: 'description' },
            { label: '状态', prop: 'status' },
          ]"
          :status="['正常', '禁用']"
          :isFixedLabel="false"
          @updateClicked="updateHandler($event)"
        ></simpleTable>
      </el-tab-pane>
      <el-tab-pane label="更多" name="9425">
        <!-- <richText
          :projects="projects9425"
          @submitClicked="submitHandler($event)"
        ></richText> -->
                <tableWithImg
          :projects="projects9441"
          :categoryId="9441"
          @showClicked="shownHandler($event)"
          @deleteClicked="deleteHandler($event)"
          @updateClicked="updateHandler($event)"
        ></tableWithImg>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import richText from "@/components/richText.vue";
import tableWithImg from "@/components/tableWithImg.vue";
import simpleTable from "@/components/simpleTable.vue";
import pageHelper from "@/utils/pageHelper";
import { mapActions, mapState } from "vuex";

export default {
  data() {
    return {
      activeName: "9441",
      tableData: [{
          date: '01',
          name: '苦瓜与猪肝',
          address: '优'
        }, {
          date: '02',
          name: '猪肚与豆芽',
          address: '优'
        }, {
          date: '03',
          name: '生姜与羊肉',
          address: '优'
        }, {
          date: '04',
          name: '鸡蛋与韭菜',
          address: '优'
        }, {
          date: '05',
          name: '啤酒和海味',
          address: '劣'
        }, {
          date: '06',
          name: '白酒和胡萝卜',
          address: '劣'
        }, {
          date: '07',
          name: '香蕉与乳酸饮料',
          address: '劣'
        }, {
          date: '08',
          name: '生姜与牛肉',
          address: '优'
        }, {
          date: '09',
          name: '苹果与茶叶、洋葱',
          address: '优'
        }, {
          date: '10',
          name: '海鲜与水果',
          address: '劣'
        }],
      tableDatas: [{
          date: '01',
          name: '优',
          address: '可为人体提供丰富的营养成分，具有清热解毒、补肝明目的功效，经常食用有利于防治癌症。'
        }, {
          date: '02',
          name: '优',
          address: '常吃可洁白皮肤及增强免疫功能，还可抗癌。 '
        }, {
          date: '03',
          name: '优',
          address: '可治腹痛、胃寒。'
        }, {
          date: '04',
          name: '优',
          address: '补肾、行气止痛'
        }, {
          date: '05',
          name: '劣',
          address: '引发痛风症'
        }, {
          date: '06',
          name: '劣',
          address: '肝脏易中毒'
        }, {
          date: '07',
          name: '劣',
          address: '产生强致癌物'
        }, {
          date: '08',
          name: '优',
          address: '可治疗伤寒腹痛'
        }, {
          date: '09',
          name: '优',
          address: '具有保护心脏的功效，减少心脏病的发病率'
        }, {
          date: '10',
          name: '劣',
          address: '影响人体对蛋白质的吸收，海鲜中的钙还会与水果中的鞣酸相结合，形成难溶的钙，会对胃肠道产生刺激，甚至引起腹痛、恶心、呕吐等症状'
        }]
    };
  },
  computed: {
    ...mapState("projectManage", [
      "projects9441",
      "projects9411",
      "projects9432",
      "projects9440",
      "projects9414",
      "projects9425",
    ]),
  },
  methods: {
    ...mapActions("projectManage", [
      "queryProject",
      "updateProject",
      "deleteProject",
    ]),
    // 处理上方模块栏变更
    moduleSwitch() {
      this.queryProject(this.activeName);
    },
    // 处理 带图片组件 的状态点击事件
    shownHandler(e) {
      // e 为子组件传出的 item,只需要更新这个 item 即可
      e.status == "正常" ? (e.status = "已完成") : (e.status = "正常");
      // 状态为已完成的项目 最多为 5 个
      if (e.categoryId == "9414") {
        // 学生风采
        let status9414 = this.projects9414.filter((i) => {
          return i.status == "已完成";
        });
        // 学生风采超过 5 个
        if (status9414.length < 6) {
          this.updateProject({ data: e, id: 9414 });
        } else {
          this.$message({
            showClose: true,
            message: "学生风采不能展示超过五名学生",
            type: "error",
          });
        }
      } else if (e.categoryId == "9441") {
        // 轮播图
        let status9441 = this.projects9441.filter((i) => {
          return i.status == "已完成";
        });
        // 轮播图超过 4 个
        if (status9441.length < 5) {
          this.updateProject({ data: e, id: 9441 });
        } else {
          this.$message({
            showClose: true,
            message: "轮播图不能展示超过四张图片",
            type: "error",
          });
        }
      } else {
        this.updateProject({ data: e, id: e.categoryId });
      }
    },
    // 删除按钮事件
    deleteHandler(e) {
      this.deleteProject({ id: e.id, cateId: e.categoryId });
    },
    // 新增按钮事件
    updateHandler(e) {
      console.log(e);
      // 此处需要把 photo JSON序列化
      e.photo = JSON.stringify(e.photo)
      this.updateProject({ data: e, id: e.categoryId });
    },
    // 富文本编辑器提交按钮事件
    submitHandler(e) {
      console.log(e);
      this.updateProject({ data: e, id: e.categoryId });
    },
  },
  components: {
    richText,
    tableWithImg,
    simpleTable,
  },
  created() {
    this.queryProject(this.activeName);
  },
};
</script>

<style>
</style>
