<template>
  <div class="home">
    <div @click.ctrl="handleDesign" :style="element.css">
      我是一个可设计的内容，请点击我进行设计吧！
    </div>

    <el-drawer
      title="设计"
      :visible.sync="designing"
      :modal="false"
      size="35%"
      class="designer-panel">
      <style-designer
        :css="designer ? designer.css : {}"></style-designer>
    </el-drawer>
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
      element: {
        css: {}
      },
      designer: null
    }
  },
  computed: {
    designing: {
      get () {
        return this.designer !== null
      },
      set (newVal) {
        this.designer = null
      }
    }
  },
  methods: {
    handleDesign () {
      this.designer = this.element
    }
  }
}
</script>

<style>
.designer-panel .el-drawer{ overflow-y: auto; }
.designer-panel .style-designer{ padding: 20px; }
</style>
