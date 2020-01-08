<template>
  <div>
    <Button @click="createPDF">Print to image</Button>
    <Button v-if="resetToggle" @click="reset">Reset page to form</Button>
    <div id="canvasholder" />
  </div>
</template>

<script>
import jsPDF from "jspdf";
import html2canvas from "html2canvas";
// var doc = new jsPDF();
import pdfMake from "pdfmake/build/pdfmake";
import pdfFonts from "pdfmake/build/vfs_fonts";
pdfMake.vfs = pdfFonts.pdfMake.vfs;

export default {
  name: "ImageMaker",

  data: () => ({
    resetToggle: false
  }),
  methods: {
    printimg() {
      //   html2canvas(document.body).then(function(canvas) {
      //     const canv = document.getElementById("canvasholder");
      //     canv.appendChild(canvas);
      doc.html(document.body, {
        callback: function(doc) {
          doc.save();
        }
      });

      this.resetToggle = true;
    },
    reset() {
      //   var canva = document.getElementsByTagName("canvas");
      //   canva.removeChild(canva);
      this.resetToggle = true;
    },
    print() {
      pdfMake.createPdf(docDefinition).open({}, window);
    },
    createPDF() {
      let pdfName = "mes-enfants";
      var doc = new jsPDF();

      doc.fromHTML(document.getElementById("content"), 15, 15, {
        width: 1000
      });

      doc.save(pdfName + ".pdf");
    }
  }
};
</script>