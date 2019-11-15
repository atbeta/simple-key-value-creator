<template>
<div class="config-item-page">
  <div class=config-list-wrapper>
    <ul class="config-list">
      <li v-for="(item, index) in configList" :key="index" class="config-list-item">
        <div class="input-wrapper">
          <Input v-model="item.source" placeholder="请输入要被替换的字段" class="input-item" />
          <Input v-model="item.value" placeholder="请输入要替换的值" class="input-item" />
        </div>
        <div class="button-wrapper">
          <Button type="primary" class="add-button" v-if="isLastItem(index)" @click="addConfigItem">增加</Button>
          <Button type="error" class="delete-button" :disabled="configList.length === 1" @click="deleteConfigItem(index)">删除</Button>
        </div>
      </li>
    </ul>
  </div>
  <div class="outer-button-wrapper">
    <Button type="primary" @click="createConfig">生成配置</Button>
    <Button type="primary" @click="importConfig">导入配置</Button>
  </div>
  <Modal
        v-model="configDialogShow"
        title="生成配置"
        @on-ok="configDialogShow = false"
        @on-cancel="configDialogShow = false">
        {{configJSON}}
    </Modal>
  <Modal
        v-model="importDialogShow"
        title="导入配置"
        @on-ok="handleImportConfig"
        @on-cancel="importDialogShow = false">
        <Input v-model="importedConfig" type="textarea" :rows="20" placeholder="请将配置文件内容粘贴至此" />
    </Modal>
</div>
</template>
<script>
export default {
  data() {
    return {
      configDialogShow: false,
      importDialogShow: false,
      configList: [
        {source: '', value: ''}
      ],
      configJSON: {},
      importedConfig: ''
    }
  },
  methods: {
    isLastItem(index) {
      return this.configList.length === index + 1
    },
    addConfigItem() {
      const emptyItem = {
        source: '',
        value: ''
      }
      this.configList.push(emptyItem)
    },
    deleteConfigItem(index) {
      this.configList.splice(index, 1)
    },
    createConfig() {
      this.configList.forEach(item => {
        this.configJSON[item.source] = item.value
      })
      this.configDialogShow = true
    },
    importConfig() {
      this.importDialogShow = true
    },
    handleImportConfig() {
      const importedConfig = JSON.parse(this.importedConfig)
      this.configList = Object.keys(importedConfig).map(key => {
        return {
          source: key,
          value: importedConfig[key]
        }
      })
    }
  }
}
</script>
<style lang="less" scoped>
.config-item-page {
  min-width: 1000px;
  .config-list-wrapper {
    width: 800px;
    margin: auto;
    .input-item {
    width: 240px;
    margin-right: 20px;
  }
  .config-list {
    .config-list-item {
      display: flex;
      width: 800px;
      margin: auto;
      margin-bottom: 6px;
      .add-button {
        margin-right: 10px;
      }
    }
  }
  }
  .outer-button-wrapper {
    width: 800px;
    margin: auto;
    margin-top: 10px;
    padding-right: 290px;
    button {
      margin-right: 10px;
    }
  }
}
</style>
