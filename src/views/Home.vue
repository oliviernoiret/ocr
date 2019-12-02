<template>
  <div class="home">
    <v-row
      justify="space-between"
    >
        <v-file-input
          hint="Choisissez un fichier pdf"
          label="Fichier pdf"
          placeholder="nom du fichier pdf"
          single-line
          chips
          clearable
          show-size
          accept=".pdf"
          :rules="limits"
          v-model="file"
        >
        </v-file-input>
        <v-btn
          color="primary"
          @click="importTextFile"
        >
        Importer
        </v-btn>
      </v-row>

      <v-row
        align="center"
      >
        <v-sheet v-if="file"
        class="ma-2 pa-2"
        elevation="8"
        >
          <p color="primary">{{ file.name }}</p>
          <p color="secondary">{{ file.size }} {{ file.lastModified }} {{ file.type }}</p>
        </v-sheet>
      </v-row>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'home',

  components: {
  },

  data () {
    return {
      limits: [ value => !value || value.size < 5000000 || 'La taille du fichier ne doit pas dépasser 5 Mo' ],
      file: null
    }
  },

  methods: {

    importTextFile () {
      console.log(this.file)

      let CloudmersiveOcrApiClient = require('cloudmersive-ocr-api-client')
      let defaultClient = CloudmersiveOcrApiClient.ApiClient.instance

      // Configure API key authorization: Apikey
      let Apikey = defaultClient.authentications['Apikey']
      Apikey.apiKey = '2b177236-13cc-4978-81c8-543721ad9819'
      // Uncomment the following line to set a prefix for the API key, e.g. "Token" (defaults to null)
      // Apikey.apiKeyPrefix = 'Token'

      let apiInstance = new CloudmersiveOcrApiClient.PdfOcrApi()

      let imageFile = this.file.webkitRelativePath + this.file.name // File | PDF file to perform OCR on.

      let opts = {
        'language': 'language_example', // String | Optional, language of the input document, default is English (ENG).  Possible values are ENG (English), ARA (Arabic), ZHO (Chinese - Simplified), ZHO-HANT (Chinese - Traditional), ASM (Assamese), AFR (Afrikaans), AMH (Amharic), AZE (Azerbaijani), AZE-CYRL (Azerbaijani - Cyrillic), BEL (Belarusian), BEN (Bengali), BOD (Tibetan), BOS (Bosnian), BUL (Bulgarian), CAT (Catalan Valencian), CEB (Cebuano), CES (Czech), CHR (Cherokee), CYM (Welsh), DAN (Danish), DEU (German), DZO (Dzongkha), ELL (Greek), ENM (Archaic/Middle English), EPO (Esperanto), EST (Estonian), EUS (Basque), FAS (Persian), FIN (Finnish), FRA (French), FRK (Frankish), FRM (Middle-French), GLE (Irish), GLG (Galician), GRC (Ancient Greek), HAT (Hatian), HEB (Hebrew), HIN (Hindi), HRV (Croatian), HUN (Hungarian), IKU (Inuktitut), IND (Indonesian), ISL (Icelandic), ITA (Italian), ITA-OLD (Old - Italian), JAV (Javanese), JPN (Japanese), KAN (Kannada), KAT (Georgian), KAT-OLD (Old-Georgian), KAZ (Kazakh), KHM (Central Khmer), KIR (Kirghiz), KOR (Korean), KUR (Kurdish), LAO (Lao), LAT (Latin), LAV (Latvian), LIT (Lithuanian), MAL (Malayalam), MAR (Marathi), MKD (Macedonian), MLT (Maltese), MSA (Malay), MYA (Burmese), NEP (Nepali), NLD (Dutch), NOR (Norwegian), ORI (Oriya), PAN (Panjabi), POL (Polish), POR (Portuguese), PUS (Pushto), RON (Romanian), RUS (Russian), SAN (Sanskrit), SIN (Sinhala), SLK (Slovak), SLV (Slovenian), SPA (Spanish), SPA-OLD (Old Spanish), SQI (Albanian), SRP (Serbian), SRP-LAT (Latin Serbian), SWA (Swahili), SWE (Swedish), SYR (Syriac), TAM (Tamil), TEL (Telugu), TGK (Tajik), TGL (Tagalog), THA (Thai), TIR (Tigrinya), TUR (Turkish), UIG (Uighur), UKR (Ukrainian), URD (Urdu), UZB (Uzbek), UZB-CYR (Cyrillic Uzbek), VIE (Vietnamese), YID (Yiddish)
        'preprocessing': 'preprocessing_example' // String | Optional, preprocessing mode, default is 'Auto'.  Possible values are None (no preprocessing of the image), and Auto (automatic image enhancement of the image before OCR is applied this is recommended).
      }

      let callback = function (error, data, response) {
        if (error) {
          console.error(error)
        } else {
          console.log('API called successfully. Returned data: ' + data)
        }
      }
      apiInstance.pdfOcrPdfToLinesWithLocation(imageFile, opts, callback)
    }
  }
}
</script>
