<template>
  <el-form
    :model="article"
    ref="ruleForm"
    label-width="80px"
    class="demo-ruleForm"
    @submit.native.prevent="saveArticle"
  >
    <el-form-item label="文章标题" prop="name">
      <el-input v-model="article.title"></el-input>
    </el-form-item>
    <el-form-item label="文章内容" prop="desc">
      <el-input type="textarea" v-model="article.body"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" native-type="submit">保存</el-button>
      <el-button @click="resetForm('ruleForm')">取消</el-button>
    </el-form-item>
  </el-form>
</template>
<script>
export default {
  data() {
    return {
      article: {
        title: '',
        body: ''
      },
      // rules: {
      //   name: [
      //     { required: true, message: "请输入活动名称", trigger: "blur" },
      //     { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" }
      //   ],
      //   region: [
      //     { required: true, message: "请选择活动区域", trigger: "change" }
      //   ],
      //   date1: [
      //     {
      //       type: "date",
      //       required: true,
      //       message: "请选择日期",
      //       trigger: "change"
      //     }
      //   ],
      //   date2: [
      //     {
      //       type: "date",
      //       required: true,
      //       message: "请选择时间",
      //       trigger: "change"
      //     }
      //   ],
      //   type: [
      //     {
      //       type: "array",
      //       required: true,
      //       message: "请至少选择一个活动性质",
      //       trigger: "change"
      //     }
      //   ],
      //   resource: [
      //     { required: true, message: "请选择活动资源", trigger: "change" }
      //   ],
      //   desc: [{ required: true, message: "请填写活动形式", trigger: "blur" }]
      // }
    };
  },
  methods: {
    saveArticle() {
      this.$http.put(`articles/${this.$route.params.id}`, this.article).then(() => {
        this.$message({
          message: '文章更新成功',
          type: 'success'
        })
        // 跳转到文章列表页
        this.$router.push('/articles/index')
      })
    },
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    fetch() {
      this.$http.get(`articles/${this.$route.params.id}`).then(res => {
        this.article = res.data
      })
    },
  },
  created () {
    this.fetch()
  }
};
</script>