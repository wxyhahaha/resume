<template>
  <div class="pdf-content-wrapper">
    <div class="title">
      <el-button class="pdf-btn" @click="upPdf()">导出PDF</el-button>
    </div>
    <div id="pdf">
      <slot></slot>
    </div>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue, Watch } from 'vue-property-decorator';

import html2canvas from 'html2canvas';
import { jsPDF } from 'jspdf';
@Component({
  name: 'Pdf',
})
export default class extends Vue {
  @Prop() private name!: string;

  private upPdf() {
    new (html2canvas as any)((document as any).getElementById('pdf')).then((canvas: any) => {
      const contentWidth = canvas.width;
      const contentHeight = canvas.height;

      // 一页pdf显示html页面生成的canvas高度;
      const pageHeight = contentWidth / 592.28 * 841.89;
      // 未生成pdf的html页面高度
      const leftHeight = contentHeight;
      // a4纸的尺寸[595.28,841.89]，html页面生成的canvas在pdf中图片的宽高
      const imgWidth = 595.28;
      const imgHeight = 592.28 / contentWidth * contentHeight;
      const pageData = canvas.toDataURL('image/jpeg', 1.0);
      const pdf = new jsPDF('' as any, 'pt', 'a4');
      pdf.addImage(pageData, 'JPEG', 0, 0, imgWidth, imgHeight );
      pdf.save(`${this.name}.pdf`);
    });
  }
}
</script>
<style scoped>
.title {
  overflow: hidden;
}
#pdf {
  height: 500px;
}
.pdf-btn {
  float: right;
}
.pdf-content-wrapper {
  padding: 16px;
}
</style>
