<template>
  <div class="style-designer">
    <el-form
     size="mini"
     label-position="left"
     label-width="120px"
     label-suffix="：">

      <el-form-item label="隐藏">
        <el-switch
          v-model="css.visibility"
          active-value="hidden"
          inactive-value="visible"></el-switch>
      </el-form-item>

      <el-form-item
        label="宽度">
        <el-input
          v-model="css.width"
          type="text"></el-input>
      </el-form-item>

      <el-form-item label="文字颜色">
        <el-color-picker
          v-model="css.color"></el-color-picker>
      </el-form-item>
      <el-form-item label="文字粗细">
        <el-radio-group v-model="css.fontWeight">
          <el-radio-button label="lighter">细</el-radio-button>
          <el-radio-button label="normal">正常</el-radio-button>
          <el-radio-button label="bolder">加粗</el-radio-button>
        </el-radio-group>
      </el-form-item>
      <el-form-item label="文字对齐">
        <el-radio-group v-model="css.textAlign">
          <el-radio-button label="left">左对齐</el-radio-button>
          <el-radio-button label="center">居中</el-radio-button>
          <el-radio-button label="right">右对齐</el-radio-button>
        </el-radio-group>
      </el-form-item>

      <el-form-item label="边框">
        <el-select
          v-model="css.borderStyle">
          <el-option value="solid" label="边框1">
            <div class="center-line" style="border: 1px solid;"></div>
          </el-option>
          <el-option value="dashed" label="边框2">
            <div class="center-line" style="border: 1px dashed;"></div>
          </el-option>
          <el-option value="dotted" label="边框3">
            <div class="center-line" style="border: 1px dotted;"></div>
          </el-option>
          <el-option value="outset" label="边框4">
            <div class="center-line" style="border: 1px outset;"></div>
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="边框宽度">
        <el-select
          v-model="css.borderWidth">
          <el-option value="1px" label="1像素">
            <div class="center-line" style="border: 1px solid;"></div>
          </el-option>
          <el-option value="2px" label="2像素">
            <div class="center-line" style="border: 2px solid;"></div>
          </el-option>
          <el-option value="3px" label="3像素">
            <div class="center-line" style="border: 3px solid;"></div>
          </el-option>
          <el-option value="4px" label="4像素">
            <div class="center-line" style="border: 4px solid;"></div>
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="边框颜色">
        <el-color-picker
          v-model="css.borderColor"></el-color-picker>
      </el-form-item>
      <el-form-item label="边框圆角">
        <el-select v-model="css.borderRadius">
          <el-option value="3px" label="小小圆角">小小圆角</el-option>
          <el-option value="5px" label="小圆角">小圆角</el-option>
          <el-option value="10px" label="中圆角">中圆角</el-option>
          <el-option value="15px" label="大圆角">大圆角</el-option>
          <el-option value="25px" label="大大圆角">大大圆角</el-option>
          <el-option value="35px" label="大大大圆角">大大大圆角</el-option>
          <el-option value="1000px" label="圆">圆</el-option>
        </el-select>
      </el-form-item>

      <el-form-item label="背景色">
        <el-color-picker
          v-model="css.backgroundColor"></el-color-picker>
      </el-form-item>

      <el-form-item label="内边距">
        <el-select v-model="css.padding">
          <el-option value="5px" label="5像素">5像素</el-option>
          <el-option value="10px" label="10像素">10像素</el-option>
          <el-option value="15px" label="15像素">15像素</el-option>
          <el-option value="20px" label="20像素">20像素</el-option>
          <el-option value="30px" label="30像素">30像素</el-option>
          <el-option value="50px" label="50像素">50像素</el-option>
        </el-select>
      </el-form-item>

    </el-form>
  </div>
</template>

<script>
export default {
  props: {
    css: {
      type: Object,
      required: true,
      default: () => {
        return {}
      }
    }
  },
  data () {
    return {
      hidden: false
    }
  },
  computed: {
  },
  watch: {
    'css.borderWidth' (newVal, oldVal) {
      if (newVal && !oldVal) {
        // this.css.borderStyle = 'solid'
        // this.css.borderColor = '#000'
      }
    }
    // hidden (newVal) {
    //   this.css.visibility = newVal ? 'hidden' : 'visible'
    // }
  },
  beforeMount () {
  },
  methods: {
    toNumber (val) {
      return parseInt(val)
    }
  }
}
</script>

<style scoped>
  .center-line{ position: absolute; left: 10%; right: 10%; top: 49%;}
</style>
