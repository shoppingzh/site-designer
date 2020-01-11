<template>
  <div class="site">
    <el-row type="flex" align="middle" class="top-nav" >
      <el-image fit="contain" class="logo" src="http://ste.dascomsoft.com/suite/template/space/common/logohere.png"></el-image>
      <div class="link">课程后台</div>
      <div class="link">网站后台</div>
      <div class="link">首页调整</div>
      <div class="link">English</div>

      <div>
        <el-button type="warning" size="mini" @click="designing = true"><i class="el-icon-s-grid"></i> 所见即所得设计</el-button>
      </div>
    </el-row>
    <el-container :style="site.css">
      <el-header class="header" style="height: auto;" :style="site.header ? site.header.css : null">
        <div class="baner" :style="site.header && site.header.banner ? site.header.banner.css : null">
          <el-image fit="fill" src="http://ste.dascomsoft.com/suite/template/module25/skin9/logo_zh_CN.gif"></el-image>
        </div>
        <el-menu
          mode="horizontal"
          background-color="rgb(24, 147, 227)"
          text-color="#f3f4f7"
          :style="site.header && site.header.navbar ? site.header.navbar.css : null">
          <el-menu-item index="0">首页</el-menu-item>
          <el-menu-item index="1">课程概要</el-menu-item>
        </el-menu>
      </el-header>
      <el-main v-if="site.main" class="main" :style="site.main.css">
        <el-row class="panels">
          <el-col v-if="site.main.left" :span="6" :style="site.main.left ? site.main.left.css : null">
            <div class="panel" v-for="panel in site.main.left.panels" :key="panel.title" :style="panel.css">
              <el-row type="flex" align="middle" class="panel-head" :style="panel.head.css">
                {{ panel.title }}
              </el-row>
              <div class="panel-body" :style="panel.body.css"></div>
            </div>
          </el-col>
          <el-col v-if="site.main.center" :span="12" :style="site.main.center ? site.main.center.css : null">
            <div class="panel" v-for="panel in site.main.center.panels" :key="panel.title" :style="panel.css">
              <el-row type="flex" align="middle" class="panel-head" :style="panel.head.css">
                {{ panel.title }}
              </el-row>
              <div class="panel-body" :style="panel.body.css"></div>
            </div>
          </el-col>
          <el-col v-if="site.main.right" :span="6" :style="site.main.right ? site.main.right.css : null">
            <div class="panel" v-for="panel in site.main.right.panels" :key="panel.title" :style="panel.css">
              <el-row type="flex" align="middle" class="panel-head" :style="panel.head.css">
                {{ panel.title }}
              </el-row>
              <div class="panel-body" :style="panel.body.css"></div>
            </div>
          </el-col>
        </el-row>
      </el-main>
      <el-footer class="footer">
      </el-footer>
    </el-container>

    <el-drawer
      :title="(designer && designer.title) ? `${designer.title} - 设计`  : '设计'"
      :visible.sync="designing"
      :modal="false"
      size="35%"
      class="designer-panel">
      <template v-if="designer === null">
        <el-tree
          default-expand-all
          :data="siteTree"
          :props="treeProps">
          <el-row type="flex" slot-scope="{ node, data }" style="width: 100%; font-size: 14px;">
            <el-col :span="24">{{ node.label }}</el-col>
            <el-link v-if="data.data.css" type="primary" style="padding: 0 5px;" :underline="false" @click="handleDesign(data.data)">设计</el-link>
          </el-row>
        </el-tree>
      </template>
      <template v-else>
        <el-row type="flex">
          <el-col :span="16">
            <el-link type="warning" :underline="false" @click="designer = null" style="padding-left: 15px;"><i class="el-icon-back"></i> 返回</el-link>
          </el-col>
          <el-col :span="8">
            <el-link type="primary" :underline="false" @click="handleStartFastApply" style="padding-right: 15px; float: right;">快速应用</el-link>
          </el-col>
        </el-row>
        <style-designer
          :css="designer ? designer.css : {}"></style-designer>
      </template>
    </el-drawer>
    <el-dialog
      title="快速应用"
      :visible.sync="fastApply">
      <el-tree
          default-expand-all
          :data="siteTree"
          :props="treeProps"
          show-checkbox
          :check-strictly="true"
          @check-change="handleFastApply">
        </el-tree>
    </el-dialog>
  </div>
</template>

<script>
import StyleDesigner from '@/components/StyleDesigner'

export default {
  name: 'home',
  components: {
    StyleDesigner
  },
  data () {
    return {
      site: {},
      designing: false,
      designer: null,
      fastApply: false,
      treeProps: {
        label: 'title',
        children: 'children'
      }
    }
  },
  computed: {
    siteTree () {
      const tree = []
      this.iterateTree(this.site, tree)
      return tree
    }
  },
  methods: {
    handleDesign (designer) {
      this.designer = designer
    },
    iterateTree (obj, tree) {
      if (!obj || typeof obj !== 'object') {
        return
      }
      if (obj.css) {
        const parent = {
          title: obj.title || `Part - ${tree.length + 1}`,
          data: obj
        }
        tree.push(parent)
        tree = []
        parent.children = tree
      }
      for (const key in obj) {
        this.iterateTree(obj[key], tree)
      }
    },
    handleStartFastApply () {
      this.fastApply = true
    },
    handleFastApply (node) {
      node.data.css = Object.assign(node.data.css, this.designer.css)
    }
  },
  mounted () {
    this.axios.get('site.json').then((resp) => {
      this.site = resp.data
    }).catch(() => {})
  }
}
</script>

<style scoped>
.site{ background-color: rgb(178, 199, 224); }

.site .top-nav{ background-color: rgb(13, 112, 202); min-height: 30px; padding: 5px 15px; }
.site .top-nav .logo{ width: 40px; height: 40px; }
.site .top-nav .link{ padding: 5px 10px; color: #fff; font-weight: normal; font-size: 14px; cursor: pointer; line-height: 30px;  }
.site .top-nav .link:hover{ text-decoration: underline; }

.site .baner{ font-size: 0; }
.site .baner .el-image{ width: 100%; }
.site .header,.site .main{ padding: 0; background-color: #fff;}

.designer-panel .el-drawer{ overflow-y: auto; }
.designer-panel .style-designer{ padding: 20px; }

.panels .panel{ margin: 5px; }
.panel{ box-sizing: border-box; border: 1px solid rgb(189, 206, 224); overflow: hidden; }
.panel .panel-head{ min-height: 35px; border-bottom: 1px solid rgb(189, 206, 224); padding: 0 5px; font-size: 16px; color: #666;  }
.panel .panel-body{ min-height: 120px; }
</style>
