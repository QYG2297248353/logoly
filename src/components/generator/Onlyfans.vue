<template>
  <div class="flex flex-col items-center">
    <v-tooltip text="编辑文字，创建自己的徽标" model-value location="top">
      <template v-slot:activator="{ props }">
        <div v-bind="props" class="box">
          <div class="editarea" id="logo" :style="{
            'font-size': fontSize + 'px',
            'background-color': transparentBgColor
          }">
            <span @input="updatePrefix" class="prefix" :style="{ color: prefixColor }" :contenteditable="store.editable"
              spellcheck="false">
              {{ store.prefix }}
            </span>
            <!-- HACK: meaningless text: ".", just to split input area, see: #269 -->
            <span style="font-size: 0">.</span>
            <span class="postfix" :style="{
              color: suffixColor,
              'background-color': postfixBgColor,
              'margin-left': suffixMargin
            }" :contenteditable="store.editable" @input="updateSuffix" spellcheck="false">{{ store.suffix }}</span>
          </div>
        </div>
      </template>
    </v-tooltip>

    <div class="w-1/3 mb-12">
      <div class="flex flex-col">
        字体大小: {{ fontSize }}px
        <div class="-ml-1">
          <v-slider hide-details min="30" max="200" step="1" color="#f90" v-model="fontSize"></v-slider>
        </div>
      </div>
      <div class="flex items-center">
        透明背景: <v-checkbox-btn v-model="transparentBg"></v-checkbox-btn>
      </div>
    </div>

    <div class="download-share">
      <ExportBtn />
      <v-btn @click="twitter" color="#1da1f2"><v-icon icon="mdi-twitter" class="mr-0.5"></v-icon>分享到推特</v-btn>
    </div>
  </div>
</template>

<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue';
import { useStore } from '@/stores/store';
import ExportBtn from '@/components/ExportBtn.vue';

const prefixColor = ref('#ffffff');
const suffixColor = ref('#00AFF0');
const postfixBgColor = ref('transparent');
const fontSize = ref(60);
const transparentBg = ref(false);
const suffixMargin = computed(() => {
  return '-' + fontSize.value / 30 + 'rem';
});

const store = useStore();

const updatePrefix = (e) => {
  if (!navigator.userAgent.toLowerCase().includes('firefox')) {
    store.updatePrefix(e.target.childNodes[0].nodeValue);
  }
};

const updateSuffix = (e) => {
  if (!navigator.userAgent.toLowerCase().includes('firefox')) {
    store.updateSuffix(e.target.childNodes[0].nodeValue);
  }
};

const twitter = () => {
  let url = 'https://blog.lifebus.top';
  let text = encodeURIComponent(`在线徽标生成器 #人生足迹 · 博客平台, by @萌森工作室 ${url}`);
  window.open(`https://twitter.com/intent/tweet?text=${text}`);
};

const transparentBgColor = computed(() => {
  if (transparentBg.value) {
    return 'transparent';
  } else {
    return '#000000';
  }
});

onMounted(() => {
  store.updatePrefix('Only');
  store.updateSuffix('Fans');
});

onBeforeUnmount(() => {
  store.updatePrefix('edit');
  store.updateSuffix('me');
});
</script>

<style lang="stylus" scoped>
.pornhub {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.box {
  border: 1px solid #333;
  border-radius: 10px;
  padding: 40px;
  margin: 40px 10px;
  max-width: 100%;

  .editarea {
    padding: 20px 30px;
    text-align: center;
    font-size: 60px;
    font-weight: 700;

    .prefix {
      color: #fff;
      padding: 5px 5px;
      font-family: "Inter", sans-serif;
      font-optical-sizing: auto;
      font-weight: 200;
      font-style: normal;
    }

    .postfix {
      color: #000;
      background-color: transparent;
      padding: 5px 10px;
      margin-left: -2rem;
      font-family: "Arizonia", cursive;
      font-weight: 400;
      font-style: normal;
    }
  }
}

.customize {
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 100%;
  margin-bottom: 50px;

  .customize-color > div,
  .customize-misc > div {
    padding: 8px 0;
  }
}

.download-share {
  display: flex;
  justify-content: space-around;
  width: 80%;

  & > div {
    width: 100px;
    height: 40px;
    border-radius: 3px;
    line-height: 40px;
    text-align: center;
    cursor: pointer;
  }

  .download {
    color: black;
    background: #f90;
  }

  .share {
    color: #fff;
    background: #1da1f2;
  }
}
</style>
