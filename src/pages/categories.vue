<template>
  <div class="page">
    <div class="wrapper">
      <el-row>
        <el-col :xs="24"
                :sm="4"
                :md="18"
                :lg="18"
                :xl="18">
          <div class="main">
            <p class="title">Categories</p>
            <list_article :items="items"
                          type="categories"></list_article>
          </div>
        </el-col>
        <el-col :xs="0"
                :sm="4"
                :md="6"
                :lg="6"
                :xl="6">
          <div class="aside">
            <p class="title">Content</p>
            <Content :items="items" />
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import Article from '@components/list_article'
import Content from '@components/list_content'
import { webUrl } from '@static/js/public.js'

export default {
  data () {
    return {
      items: []
    }
  },
  components: {
    Article,
    Content
  },
  created () {
    // this.$axios.get('http://localhost:8080/static/goods.json').then((data)=>{
    // // this.$axios.get('./static/goods.json').then((data)=>{
    //   console.log(data)
    //   this.items=data.data.categories;
    // })
    this.$axios.post(webUrl + 'articleList', { 'type': 'categories' })
      .then((res) => {
        this.items = res.data
      })
  }
}
</script>

<style lang="scss" scoped>
.main {
  background: #f8f8fd;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.4), 0 0 30px rgba(10, 10, 0, 0.1) inset;
  margin: 0 10px;
  padding: 10px;
  > .title {
    font-size: 18px;
    border-bottom: 1px solid #eee;
    padding: 5px 0;
  }
}
.aside {
  background: #f8f8fd;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.4), 0 0 30px rgba(10, 10, 0, 0.1) inset;
  > .title {
    font-size: 16px;
    font-weight: 600;
    border-bottom: 1px solid #ddd;
    padding: 10px 15px;
  }
}

@media (min-width: 768px) {
  //pc
  .main {
    margin: 0 20px;
    padding: 20px;
    > .title {
      font-size: 30px;
    }
  }
}
</style>
