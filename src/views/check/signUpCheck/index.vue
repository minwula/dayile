<template>
  <div>
    <el-tabs v-model="activeName" @tab-click="moduleSwitch">
      <!-- name属性对应着 栏目ID，通过它查找 内容 -->
      <el-tab-pane label="谷类及薯类" name="9441">
<el-table
    :data="tableData"
    border
    style="width: 100%">
    <el-table-column
      prop="date"
      label="编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="名称"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="功效">
    </el-table-column>
  </el-table>
      </el-tab-pane>
      <el-tab-pane label="动物性食物" name="9411">
<el-table
    :data="tableData1"
    border
    style="width: 100%">
    <el-table-column
      prop="date"
      label="编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="名称"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="功效">
    </el-table-column>
  </el-table>
      </el-tab-pane>
      <el-tab-pane label="豆类、坚果类" name="9432">
<el-table
    :data="tableData2"
    border
    style="width: 100%">
    <el-table-column
      prop="date"
      label="编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="名称"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="功效">
    </el-table-column>
  </el-table>
      </el-tab-pane>
      <el-tab-pane label="蔬菜、水果、菌藻类" name="9440">
  <el-table
    :data="tableData3"
    border
    style="width: 100%">
    <el-table-column
      prop="date"
      label="编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="名称"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="功效">
    </el-table-column>
  </el-table>
      </el-tab-pane>
      <el-tab-pane label="纯能量食物" name="9414">
       <el-table
    :data="tableData4"
    border
    style="width: 100%">
    <el-table-column
      prop="date"
      label="编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="名称"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="功效">
    </el-table-column>
  </el-table>
      </el-tab-pane>
      <!-- <el-tab-pane label="关于我们" name="9425">
        <richText
          :projects="projects9425"
          @submitClicked="submitHandler($event)"
        ></richText>
      </el-tab-pane> -->
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
       tableData: [{
          date: '01',
          name: '米',
          address: '补中益气，提供丰富的维生素、谷维素、蛋白质、花青素等营养成分'
        }, {
          date: '02',
          name: '面',
          address: '有养心益肾、健脾厚肠的功效，含有丰富的糖 蛋白质 钙 铁 磷等矿物质'
        }, {
          date: '03',
          name: '杂粮',
          address: '不仅维生素、矿物质等营养价值比白米、白面更高，而且有助于预防糖尿病、心血管疾病、肥胖和某些癌症等'
        }, {
          date: '04',
          name: '马铃薯',
          address: '马铃薯中含有丰富的蛋白质，能增加人体抵抗力，提高机体免疫力，马铃薯含有钾，可以促进身体内钠的排出，调节机体酸碱平衡，有降低血压的功效。'
        }, {
          date: '05',
          name: '甘薯',
          address: '益气健脾；养阴补肾。'
        }],
        tableData1: [{
          date: '01',
          name: '肉',
          address: '肉类食物中最有营养价值的营养素是蛋白质，平均含量为 1 0 % ～ 2 0 % ，并且更加易于人体的吸收'
        }, {
          date: '02',
          name: '禽',
          address: '优'
        }, {
          date: '03',
          name: '鱼',
          address: '鱼类富含优质蛋白，易消化吸收，脂肪含量低，还含有钙、磷、钾、碘、锌、硒等无机盐，以及维生素A、维生素D及B族维生素等，常吃鱼可以降低胆固醇'
        }, {
          date: '04',
          name: '奶',
          address: '奶类的营养成分齐全且组成比例适宜，容易被人体消化吸收，是儿童、体弱、年老者和病人的较理想食物'
        }, {
          date: '05',
          name: '蛋',
          address: '鸡蛋含有丰富的蛋白质、脂肪、维生素和铁、钙、钾等人体所需要的矿物质，蛋白质为优质蛋白，对肝脏组织损伤有修复作用；且富含DHA和卵磷脂、卵黄素，对神经系统和身体发育有利，能健脑益智，改善记忆力，并促进肝细胞再生。'
        }],
        tableData2: [{
          date: '01',
          name: '大豆',
          address: '对于患有高血压的患者还有降血压的作用，同时还能预防老年痴呆症，增强抵抗力'
        }, {
          date: '02',
          name: '干豆类',
          address: '对于患有高血压的患者还有降血压的作用，同时还能预防老年痴呆症，增强抵抗力'
        }, {
          date: '03',
          name: '花生',
          address: '花生富含有锌元素、蛋白质、氨基酸，能够促进大脑发育、提高记忆力，能够促进胃肠消化，预防出现消化不良，同时有预防肿瘤的作用'
        }, {
          date: '04',
          name: '坚果',
          address: '蛋白质、油脂、矿物质、维生素较高，对人体生长发育、增强体质、预防疾病有极好的功效。每周食用两次以上坚果能够降低人们患致命心脏病的风险'
        }, {
          date: '05',
          name: '杏仁',
          address: '杏仁是一个常用的止咳平喘的药物，第一个作用就是治疗风寒、风热、燥热引起的咳喘、痰多；第二个它可以润肠通便，肠燥便秘的病人可以应用'
        }],
        tableData3: [{
          date: '01',
          name: '蔬菜',
          address: '具有一定的抗氧化和防癌作用，其中含有葡萄糖异硫氰酸盐、维生素C、维生素E对预防营养代谢性慢病有帮助。'
        }, {
          date: '02',
          name: '水果',
          address: '含有很多维生素和微量元素，丰富的食物纤维，还有丰富的抗氧化物质，可以预防疾病，还能增进消化，改善心肌功能，对维持人体内酸碱平衡起着调节作用'
        }, {
          date: '03',
          name: '藻类（海带、紫菜...）',
          address: '含有多种有机物和碘,钾,钙,铁元素,还有蛋白质,脂肪酸,糖类,以及多种维生素和尼克酸等.它的的功效是消痰软坚,泄热利水,止渴平喘,祛脂降压,散结抗癌.'
        }, {
          date: '04',
          name: '菌类（蘑菇...）',
          address: '菌类食品有良好的抗癌作用，并且能清洁血液、扫除血液中的毒素。特别是黑木耳，其胶质有很强的吸附才华，有消化纤维和滑润肠道的作用，对增进健康极为有益。'
        }],
        tableData4: [{
          date: '01',
          name: '植物油',
          address: '吃植物油的好处非常的多，因为植物油中含有丰富的不饱和脂肪酸，既然植物油中含有丰富的不饱和脂肪酸，有降低胆固醇、软化血管、防止动脉硬化的作用。'
        }, {
          date: '02',
          name: '动物油',
          address: '动物油的性质是甘，微寒，无毒。还有一个功能就是解毒，能够解斑蝥，芫青毒，解地胆，亭长，野葛，硫磺毒，诸肝毒。动物油的第二个功能是解五种疸疾，黄疸，谷疸，酒疸，黑疸，女劳疸，还有这几种疸疾带来的水肿'
        }, {
          date: '03',
          name: '淀粉',
          address: '淀粉的主要成分是葡萄糖聚合物，是人体的主要能源来源之一，能够缓解低血糖'
        }, {
          date: '04',
          name: '食用糖',
          address: '优'
        }, {
          date: '05',
          name: '酒类',
          address: '酒中具有抗氧化的成份，降低皮肤细胞的老化速度，加速血液循环，提高对血液中垃圾毒素的排除速度，使得皮肤由内到外更健康，从而达到了美容养颜效果。'
        }],
      activeName: "9441",
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
