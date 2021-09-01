<template>
  <div>
    <button @click="printDownload">Print Download</button>
    <Download v-show="false" ref="DownloadComp" :values="values"/>
  </div>
</template>

<script>
  import Download from './components/Download'
  export default {
    data() {
      return {
        values: {
          name: 'Abhishek', 
          age: 26
        }
      }
    },
    components: {
      Download,
    },
    methods: {
      printDownload () {
        let w = window.open('','printwindow');
        w.document.write(`<html>
          <head>
            <title>Print it!</title>
            <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
            <style>
              #print {background: red;}
              .text-green { color: green;}
              .text-bold {font-weight: bold;}
              * {
                -webkit-print-color-adjust: exact !important;   /* Chrome, Safari, Edge */
                color-adjust: exact !important;                 /*Firefox*/
              }
            </style>
          </head>
          <body>`);
        w.document.write(this.$refs.DownloadComp.$el.innerHTML);
        w.document.write('</body></html>');
        w.document.close();
        w.setTimeout(function () {
          w.print()
          w.close()
        }, 1000)
      },
    },
  }
</script>
