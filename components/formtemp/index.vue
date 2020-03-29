<template>
  <component
    :is="getComponent(column.type,column.component)"
    :action="column.action"
    :append="column.append"
    :accordion="column.accordion"
    :allow-create="column.allowCreate"
    :autocomplete="column.autocomplete"
    :autofocus="column.autofocus"
    :autoUpload="column.autoUpload"
    :accept="column.accept"
    :activeColor="column.activeColor"
    :border="column.border"
    :button="column.button"
    :children="column.children"
    :checked="column.checked"
    :clearable="column.clearable"
    :column="column"
    :colors="column.colors"
    :canvasOption="column.canvasOption"
    :controls-position="column.controlsPosition"
    :checkStrictly="column.checkStrictly"
    :collapseTags="column.collapseTags"
    :data="column.data"
    :dataType="column.dataType"
    :defaultCheckedKeys="column.defaultCheckedKeys"
    :defaultExpandedKeys="column.defaultExpandedKeys"
    :defaultExpandAll="column.defaultExpandAll"
    :defaultTime="column.defaultTime"
    :dic="dic"
    :dicData="column.dicData"
    :dicUrl="column.dicUrl"
    :dicMethod="column.dicMethod"
    :dicQuery="column.dicQuery"
    :disabled="disabled"
    :drag="column.drag"
    :default-value="column.defaultValue"
    :default-time="column.defaultTime"
    :default-first-option="column.defaultFirstOption"
    :endPlaceholder="column.endPlaceholder"
    :filter="column.filter"
    :filesize="column.filesize"
    :filterable="column.filterable"
    :format="column.format"
    :formatTooltip="column.formatTooltip"
    :iconClasses="column.iconClasses"
    :iconList="column.iconList"
    :inactiveColor="column.inactiveColor"
    :group="column.group"
    :label="column.label"
    :limit="column.limit"
    :listType="column.listType"
    :loadText="column.loadText"
    :min="column.min"
    :max="column.max"
    :minlength="column.minlength"
    :maxlength="column.maxlength"
    :minRows="column.minRows"
    :maxRows="column.maxRows"
    :multiple="column.multiple"
    :options="column.options"
    :oss="column.oss"
    :onRemove="column.onRemove"
    :parent="column.parent"
    :pickerOptions="column.pickerOptions"
    :placeholder="getPlaceholder(column,column.type,disabled)"
    :precision="column.precision"
    :prefixIcon="column.prefixIcon"
    :prefix="column.prefix"
    :prepend="column.prepend"
    :prependslot="column.prependslot"
    :appendslot="column.appendslot"
    :prop="column.prop"
    :props="column.props || props"
    :propsHttp="column.propsHttp || propsHttp"
    :showPassword="column.showPassword"
    :readonly="column.readonly"
    :remote="column.remote"
    :remoteOptions="column.remoteOptions"
    :range="column.range"
    :showFileList="column.showFileList"
    :showInput="column.showInput"
    :showStops="column.showStops"
    :showAllLevels="column.showAllLevels"
    :showText="column.showText"
    :size="column.size || size"
    :startPlaceholder="column.startPlaceholder"
    :step="column.step"
    :suffix="column.suffix"
    :suffixIcon="column.suffixIcon"
    :showWordLimit="column.showWordLimit"
    :separator="column.separator"
    :texts="column.texts"
    :tip="column.tip"
    :type="column.type"
    :typeslot="column.typeslot"
    :typeformat="column.typeformat"
    :rawtype="column.rawtype"
    :upload-before="uploadBefore"
    :upload-after="uploadAfter"
    :value-format="column.valueFormat"
    :voidIconClass="column.voidIconClass"
    v-model="text"
    @change="handleChange"
    :appendClick="column.appendClick"
    :blur="column.blur"
    :click="column.click"
    :change="column.change"
    :changeOnSelect="column.changeOnSelect"
    :changeoOnSelect="column.changeoOnSelect"
    :expand-trigger="column.expandTrigger"
    :focus="column.focus"
    :prependClick="column.prependClick"
    :nodeClick="column.nodeClick"
    :isCrud="isCrud"
  >
    <template
      :slot="column.prop+'Type'"
      slot-scope="{item,labelkey,valuekey,childrenkey,node}"
      v-if="column.typeslot"
    >
      <slot
        :name="column.prop+'Type'"
        :node="node"
        :item="item"
        :valuekey="valuekey"
        :labelkey="labelkey"
        :childrenkey="childrenkey"
      ></slot>
    </template>
    <!-- input的slot处睆 -->
    <template v-if="column.prependslot" :slot="column.prependslot" slot-scope="{prependClick}">
      <slot :name="column.prependslot" :prependClick="prependClick"></slot>
    </template>
    <template v-if="column.appendslot" :slot="column.appendslot" slot-scope="{appendClick}">
      <slot :name="column.appendslot" :appendClick="appendClick"></slot>
    </template>
  </component>
</template>

<script>
import { getComponent, getPlaceholder } from "../../utils/dataformat";
import { validatenull } from "../../utils/validate";

export default {
  name: "formTemp",
  props: {
    value: [Array, String, Number, Object, Boolean, Date],
    t: Function,
    uploadBefore: Function,
    uploadAfter: Function,
    props: {
      type: Object
    },
    clearable: {
      type: Boolean
    },
    propsHttp: {
      type: Object,
      default: () => {
        return {};
      }
    },
    props: {
      type: Object
    },
    dic: {
      type: Array
    },
    placeholder: {
      type: String
    },
    size: {
      type: String
    },
    disabled: {
      type: Boolean
    },
    column: {
      type: Object,
      default: () => {
        return {};
      }
    },
    isCrud: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      first: true,
      text: null
    };
  },
  watch: {
    text: {
      handler(val) {
        if (!this.first || !validatenull(val)) {
          this.first = false;
          this.$emit("input", val);
        } else {
          this.first = false;
        }
      }
    },
    value: {
      handler(val) {
        this.text = val;
      },
      immediate: true
    }
  },
  methods: {
    getComponent,
    getPlaceholder,
    validatenull,
    handleChange(val) {
      this.$emit("change", val);
    }
  }
};
</script>