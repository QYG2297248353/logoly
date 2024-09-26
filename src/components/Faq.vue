<template>
  <div class="text-white mt-12">
    <h3 class="text-2xl font-semibold text-custom-primary mb-1">常见问题</h3>
    <v-expansion-panels variant="accordion" mandatory="force">
      <v-expansion-panel title="如何使用生成器?">
        <template v-slot:text>
          生成器的使用非常简单。只需 4 个步骤，你就能得到一个徽标：
          <ul class="list-disc mt-2">
            <div class="ml-5">
              <li>选择一个样式 (例如: 水平/垂直, Pornhub/OnlyFans/...)</li>
              <li>编辑中心框中的文字</li>
              <li>自定义徽标（颜色、背景、字体大小等）</li>
              <li>最后，点击 "导出 "按钮，就能得到属于自己的徽标了</li>
            </div>
          </ul>
        </template>
      </v-expansion-panel>
      <v-expansion-panel text="生成的徽标完全属于您。您可以为任何目的自由使用它。但请务必注明出处。" title="能否将生成的徽标用于个人或商业用途？"></v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>
