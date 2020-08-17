<template>
  <v-app :dark="mode">
    <v-layout px-2 row wrap>
      <v-flex xs12 md12>
        <v-btn @click="showPreviews">Show Previews</v-btn>
      </v-flex>
      <v-flex
        md6
        v-for="(iframe, index) in iframes"
        :key="index"
        id="card-parent"
        :class="{'pa-0':$vuetify.breakpoint.smAndDown}"
      >
        <v-card id="card-parent-2" :key="`${index}${$vuetify.breakpoint.width}`" flat>
          <div class="preview-card" :key="`${index}${$vuetify.breakpoint.width}`" v-html="iframe"/>
        </v-card>
      </v-flex>
    </v-layout>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      drawer: false,
      mode: false,
      iframes: [],
      pattern: '/src=([^\\"]+)/'
    };
  },
  methods: {
    showPreviews() {
      let response = [
        {
          body:
            '<iframe src="https://www.facebook.com/ads/api/preview_iframe.php?d=AQINR98fmsIvXhblliawS8Jph_lhrWpQfUro1wjwLn0LypJ5hIJcKjr5WIJs3N-U2Jmn2dyV1nJqvsoQK9vPCC6pWMXIdFzdtxlsTTks7GsMT3AHagZ_8NA9P-gfra_u1iFVAQAjUtaFr6-nZ01KwE_1LtZTi3vdknWSzVpi1DK3qC_ZtdhF1ncwCQLNgdZVTMhBB4sXMNEQ-xS4kcz5OOnr3Ihzs7Yl5EioGzih_XRBEtBpjHWszW39TTfYlS7QjxNl3ItgtNyi0gaqgVFVb9vgz1bNLle2dLreCamxotDNEZKLPRqdPQ7X8Grx1NSxKFMpvqsXjsaIwnp0sw2AzYG7On_IxPFr2jx4iFpO4lJpdNwA_RiL_dZZkCDrl91wrFHgV6o7x2maY7xpNvANPw3HtWZ1AqHUPa7BzGPBCVvmrup1ps-w066ub4L84Sfszt96PG2BjjvDkqIdhfjj2cskfHI2LoqK5dtHKBrhbJZx0PzFTBpP5ez3qeE9QVr9GG1My8rGcoGqAN_MRkpgLvZHcsW6moY4UjTRXAv1iF4v-8mv_n090SIvbiBuJ-wzsIwP4O9eZsoj5GBAL_ud7KnEieHBRVyN2X7ne6dBq90_I7qIw_H8ZitI-3e9VXnOexRTTEYVsCfZh74KWcfioTOuQAEnJyNnE28MiccLCauYbNJJVdQhYPsEipayQJKWhgAJ0CGPTCHdfg05JVZpWo29wW2kxVT9jfF9GIUKpkrU9tZxMZsT5eK-Nhjk7l6RbOGjgj4K1oZgFH_nppE0wkhrAGgqohXoLsPObRWWlmCikU0EWHa2prz-uvo9_UgXcPOqshbth9Sx6aLdMC_hWrXuoO_drrJey8orF9Y6jDVkmJDXo0GXegkupZpFIodKZbj9ThG09Fx59J_2LJ9kc6UNKfWjmJLJORYTotr9daglQTHjsU9MDUnSSZdp40WMgsnDU3eFOtj5SONLDuR7PpDqg2v9n_9Ffz-Yry8aDRP9YpKKX29rNJJSIlb-SIx0EXAdLWUIeGO8ekT0XGWgrT6HP30pUBSf501nGYTb7sIpO-sB23yabyUVfGzkozl2fkk1hZsGkOFt8cwhYzXogg3NT3k6rvOmRmlUgE9-Y7kOLl0Wc6HfjMUo6w7r8qzvzVLEkUXG6IQA01fUtBZil9Ilaea-VBR4D9Q1QOnxygSiEHTrC9EaRu7lUgvWldcZEJdTR1Ef_QxMJCbkZsHo5REoQQp09MI5uXcv-Z8NdwPRwX_vCG6sqER9_xNZ0awVZ8r5kNotAyCPzr-lsMcqUnZatcpfn9oz4htsJdn4wwHu566xP5wChD0rsdRaNytMJ09Pt8zUFoB8y9WqzL8bF3BRla2eozjfSD2EOXVmu-YHX-lgkZgp1Ppt4tBt5wVNMg6lGJ2KWHtkCTR9hsdxPWOpp20xPplKw367NUaZL-anhAijwbKQ69ymOHvWA8BPaMQJOIEQp7VppPFirTW3DapF4GfIFjhJGfKEgNoz5n_xPvuT4HN5XK6ND_sxdDeemhcTl1EtPbG5QRxI9Xs5Nn7J-rIjdKOYVBZQhWd3PQOOk_KNgltetY-8mEuvKPgNhZ2yZJVuUK5jA2uGyUiIeFGmDlLLJ1QIg2M0tOZIdMVE0y4Z8e7bykIDM1sedCp9hgwmd2lsQ3io_q5adwqvg1jTki3d32cO7Cpk3cmo0zAYJTTv1K2pyYPvnTJRMkDG3GdV247-MKfjEgFclIJ7BqYaALKzsjKbumkPzKlT5NYpIDhPqPcY03deWGU3XusM0wGMF19uuoP9W1pIaBsqG7kvSJq0i__axUa3-cqrzdXOj9SG1Pyx6HwUBEdYanRohq9V1Nwhymz4guFgm0Hk4jg0yOpt3a-5NH0lId3VZMKp2bzcqaj35I35WRPKQeHnmwVvqs-CaRVRjfmi3KciRppSH8guQKK9ZrnOu84VbM3FW7bM2EOwFEsMrS6ZShR-GE2Lp5QZe_3ZV-_66DXV7Qbj&amp;t=AQJxtLreSDKkEAVK" width="540" height="690" scrolling="yes" style="border: none;"></iframe>'
        },
        {
          body:
            '<iframe src="https://www.facebook.com/ads/api/preview_iframe.php?d=AQINR98fmsIvXhblliawS8Jph_lhrWpQfUro1wjwLn0LypJ5hIJcKjr5WIJs3N-U2Jmn2dyV1nJqvsoQK9vPCC6pWMXIdFzdtxlsTTks7GsMT3AHagZ_8NA9P-gfra_u1iFVAQAjUtaFr6-nZ01KwE_1LtZTi3vdknWSzVpi1DK3qC_ZtdhF1ncwCQLNgdZVTMhBB4sXMNEQ-xS4kcz5OOnr3Ihzs7Yl5EioGzih_XRBEtBpjHWszW39TTfYlS7QjxNl3ItgtNyi0gaqgVFVb9vgz1bNLle2dLreCamxotDNEZKLPRqdPQ7X8Grx1NSxKFMpvqsXjsaIwnp0sw2AzYG7On_IxPFr2jx4iFpO4lJpdNwA_RiL_dZZkCDrl91wrFHgV6o7x2maY7xpNvANPw3HtWZ1AqHUPa7BzGPBCVvmrup1ps-w066ub4L84Sfszt96PG2BjjvDkqIdhfjj2cskfHI2LoqK5dtHKBrhbJZx0PzFTBpP5ez3qeE9QVr9GG1My8rGcoGqAN_MRkpgLvZHcsW6moY4UjTRXAv1iF4v-8mv_n090SIvbiBuJ-wzsIwP4O9eZsoj5GBAL_ud7KnEieHBRVyN2X7ne6dBq90_I7qIw_H8ZitI-3e9VXnOexRTTEYVsCfZh74KWcfioTOuQAEnJyNnE28MiccLCauYbNJJVdQhYPsEipayQJKWhgAJ0CGPTCHdfg05JVZpWo29wW2kxVT9jfF9GIUKpkrU9tZxMZsT5eK-Nhjk7l6RbOGjgj4K1oZgFH_nppE0wkhrAGgqohXoLsPObRWWlmCikU0EWHa2prz-uvo9_UgXcPOqshbth9Sx6aLdMC_hWrXuoO_drrJey8orF9Y6jDVkmJDXo0GXegkupZpFIodKZbj9ThG09Fx59J_2LJ9kc6UNKfWjmJLJORYTotr9daglQTHjsU9MDUnSSZdp40WMgsnDU3eFOtj5SONLDuR7PpDqg2v9n_9Ffz-Yry8aDRP9YpKKX29rNJJSIlb-SIx0EXAdLWUIeGO8ekT0XGWgrT6HP30pUBSf501nGYTb7sIpO-sB23yabyUVfGzkozl2fkk1hZsGkOFt8cwhYzXogg3NT3k6rvOmRmlUgE9-Y7kOLl0Wc6HfjMUo6w7r8qzvzVLEkUXG6IQA01fUtBZil9Ilaea-VBR4D9Q1QOnxygSiEHTrC9EaRu7lUgvWldcZEJdTR1Ef_QxMJCbkZsHo5REoQQp09MI5uXcv-Z8NdwPRwX_vCG6sqER9_xNZ0awVZ8r5kNotAyCPzr-lsMcqUnZatcpfn9oz4htsJdn4wwHu566xP5wChD0rsdRaNytMJ09Pt8zUFoB8y9WqzL8bF3BRla2eozjfSD2EOXVmu-YHX-lgkZgp1Ppt4tBt5wVNMg6lGJ2KWHtkCTR9hsdxPWOpp20xPplKw367NUaZL-anhAijwbKQ69ymOHvWA8BPaMQJOIEQp7VppPFirTW3DapF4GfIFjhJGfKEgNoz5n_xPvuT4HN5XK6ND_sxdDeemhcTl1EtPbG5QRxI9Xs5Nn7J-rIjdKOYVBZQhWd3PQOOk_KNgltetY-8mEuvKPgNhZ2yZJVuUK5jA2uGyUiIeFGmDlLLJ1QIg2M0tOZIdMVE0y4Z8e7bykIDM1sedCp9hgwmd2lsQ3io_q5adwqvg1jTki3d32cO7Cpk3cmo0zAYJTTv1K2pyYPvnTJRMkDG3GdV247-MKfjEgFclIJ7BqYaALKzsjKbumkPzKlT5NYpIDhPqPcY03deWGU3XusM0wGMF19uuoP9W1pIaBsqG7kvSJq0i__axUa3-cqrzdXOj9SG1Pyx6HwUBEdYanRohq9V1Nwhymz4guFgm0Hk4jg0yOpt3a-5NH0lId3VZMKp2bzcqaj35I35WRPKQeHnmwVvqs-CaRVRjfmi3KciRppSH8guQKK9ZrnOu84VbM3FW7bM2EOwFEsMrS6ZShR-GE2Lp5QZe_3ZV-_66DXV7Qbj&amp;t=AQJxtLreSDKkEAVK" width="540" height="690" scrolling="yes" style="border: none;"></iframe>'
        },
        {
          body:
            '<iframe src="https://www.facebook.com/ads/api/preview_iframe.php?d=AQINR98fmsIvXhblliawS8Jph_lhrWpQfUro1wjwLn0LypJ5hIJcKjr5WIJs3N-U2Jmn2dyV1nJqvsoQK9vPCC6pWMXIdFzdtxlsTTks7GsMT3AHagZ_8NA9P-gfra_u1iFVAQAjUtaFr6-nZ01KwE_1LtZTi3vdknWSzVpi1DK3qC_ZtdhF1ncwCQLNgdZVTMhBB4sXMNEQ-xS4kcz5OOnr3Ihzs7Yl5EioGzih_XRBEtBpjHWszW39TTfYlS7QjxNl3ItgtNyi0gaqgVFVb9vgz1bNLle2dLreCamxotDNEZKLPRqdPQ7X8Grx1NSxKFMpvqsXjsaIwnp0sw2AzYG7On_IxPFr2jx4iFpO4lJpdNwA_RiL_dZZkCDrl91wrFHgV6o7x2maY7xpNvANPw3HtWZ1AqHUPa7BzGPBCVvmrup1ps-w066ub4L84Sfszt96PG2BjjvDkqIdhfjj2cskfHI2LoqK5dtHKBrhbJZx0PzFTBpP5ez3qeE9QVr9GG1My8rGcoGqAN_MRkpgLvZHcsW6moY4UjTRXAv1iF4v-8mv_n090SIvbiBuJ-wzsIwP4O9eZsoj5GBAL_ud7KnEieHBRVyN2X7ne6dBq90_I7qIw_H8ZitI-3e9VXnOexRTTEYVsCfZh74KWcfioTOuQAEnJyNnE28MiccLCauYbNJJVdQhYPsEipayQJKWhgAJ0CGPTCHdfg05JVZpWo29wW2kxVT9jfF9GIUKpkrU9tZxMZsT5eK-Nhjk7l6RbOGjgj4K1oZgFH_nppE0wkhrAGgqohXoLsPObRWWlmCikU0EWHa2prz-uvo9_UgXcPOqshbth9Sx6aLdMC_hWrXuoO_drrJey8orF9Y6jDVkmJDXo0GXegkupZpFIodKZbj9ThG09Fx59J_2LJ9kc6UNKfWjmJLJORYTotr9daglQTHjsU9MDUnSSZdp40WMgsnDU3eFOtj5SONLDuR7PpDqg2v9n_9Ffz-Yry8aDRP9YpKKX29rNJJSIlb-SIx0EXAdLWUIeGO8ekT0XGWgrT6HP30pUBSf501nGYTb7sIpO-sB23yabyUVfGzkozl2fkk1hZsGkOFt8cwhYzXogg3NT3k6rvOmRmlUgE9-Y7kOLl0Wc6HfjMUo6w7r8qzvzVLEkUXG6IQA01fUtBZil9Ilaea-VBR4D9Q1QOnxygSiEHTrC9EaRu7lUgvWldcZEJdTR1Ef_QxMJCbkZsHo5REoQQp09MI5uXcv-Z8NdwPRwX_vCG6sqER9_xNZ0awVZ8r5kNotAyCPzr-lsMcqUnZatcpfn9oz4htsJdn4wwHu566xP5wChD0rsdRaNytMJ09Pt8zUFoB8y9WqzL8bF3BRla2eozjfSD2EOXVmu-YHX-lgkZgp1Ppt4tBt5wVNMg6lGJ2KWHtkCTR9hsdxPWOpp20xPplKw367NUaZL-anhAijwbKQ69ymOHvWA8BPaMQJOIEQp7VppPFirTW3DapF4GfIFjhJGfKEgNoz5n_xPvuT4HN5XK6ND_sxdDeemhcTl1EtPbG5QRxI9Xs5Nn7J-rIjdKOYVBZQhWd3PQOOk_KNgltetY-8mEuvKPgNhZ2yZJVuUK5jA2uGyUiIeFGmDlLLJ1QIg2M0tOZIdMVE0y4Z8e7bykIDM1sedCp9hgwmd2lsQ3io_q5adwqvg1jTki3d32cO7Cpk3cmo0zAYJTTv1K2pyYPvnTJRMkDG3GdV247-MKfjEgFclIJ7BqYaALKzsjKbumkPzKlT5NYpIDhPqPcY03deWGU3XusM0wGMF19uuoP9W1pIaBsqG7kvSJq0i__axUa3-cqrzdXOj9SG1Pyx6HwUBEdYanRohq9V1Nwhymz4guFgm0Hk4jg0yOpt3a-5NH0lId3VZMKp2bzcqaj35I35WRPKQeHnmwVvqs-CaRVRjfmi3KciRppSH8guQKK9ZrnOu84VbM3FW7bM2EOwFEsMrS6ZShR-GE2Lp5QZe_3ZV-_66DXV7Qbj&amp;t=AQJxtLreSDKkEAVK" width="540" height="690" scrolling="yes"></iframe>'
        },

        {
          body:
            '<iframe src="https://www.facebook.com/ads/api/preview_iframe.php?d=AQINR98fmsIvXhblliawS8Jph_lhrWpQfUro1wjwLn0LypJ5hIJcKjr5WIJs3N-U2Jmn2dyV1nJqvsoQK9vPCC6pWMXIdFzdtxlsTTks7GsMT3AHagZ_8NA9P-gfra_u1iFVAQAjUtaFr6-nZ01KwE_1LtZTi3vdknWSzVpi1DK3qC_ZtdhF1ncwCQLNgdZVTMhBB4sXMNEQ-xS4kcz5OOnr3Ihzs7Yl5EioGzih_XRBEtBpjHWszW39TTfYlS7QjxNl3ItgtNyi0gaqgVFVb9vgz1bNLle2dLreCamxotDNEZKLPRqdPQ7X8Grx1NSxKFMpvqsXjsaIwnp0sw2AzYG7On_IxPFr2jx4iFpO4lJpdNwA_RiL_dZZkCDrl91wrFHgV6o7x2maY7xpNvANPw3HtWZ1AqHUPa7BzGPBCVvmrup1ps-w066ub4L84Sfszt96PG2BjjvDkqIdhfjj2cskfHI2LoqK5dtHKBrhbJZx0PzFTBpP5ez3qeE9QVr9GG1My8rGcoGqAN_MRkpgLvZHcsW6moY4UjTRXAv1iF4v-8mv_n090SIvbiBuJ-wzsIwP4O9eZsoj5GBAL_ud7KnEieHBRVyN2X7ne6dBq90_I7qIw_H8ZitI-3e9VXnOexRTTEYVsCfZh74KWcfioTOuQAEnJyNnE28MiccLCauYbNJJVdQhYPsEipayQJKWhgAJ0CGPTCHdfg05JVZpWo29wW2kxVT9jfF9GIUKpkrU9tZxMZsT5eK-Nhjk7l6RbOGjgj4K1oZgFH_nppE0wkhrAGgqohXoLsPObRWWlmCikU0EWHa2prz-uvo9_UgXcPOqshbth9Sx6aLdMC_hWrXuoO_drrJey8orF9Y6jDVkmJDXo0GXegkupZpFIodKZbj9ThG09Fx59J_2LJ9kc6UNKfWjmJLJORYTotr9daglQTHjsU9MDUnSSZdp40WMgsnDU3eFOtj5SONLDuR7PpDqg2v9n_9Ffz-Yry8aDRP9YpKKX29rNJJSIlb-SIx0EXAdLWUIeGO8ekT0XGWgrT6HP30pUBSf501nGYTb7sIpO-sB23yabyUVfGzkozl2fkk1hZsGkOFt8cwhYzXogg3NT3k6rvOmRmlUgE9-Y7kOLl0Wc6HfjMUo6w7r8qzvzVLEkUXG6IQA01fUtBZil9Ilaea-VBR4D9Q1QOnxygSiEHTrC9EaRu7lUgvWldcZEJdTR1Ef_QxMJCbkZsHo5REoQQp09MI5uXcv-Z8NdwPRwX_vCG6sqER9_xNZ0awVZ8r5kNotAyCPzr-lsMcqUnZatcpfn9oz4htsJdn4wwHu566xP5wChD0rsdRaNytMJ09Pt8zUFoB8y9WqzL8bF3BRla2eozjfSD2EOXVmu-YHX-lgkZgp1Ppt4tBt5wVNMg6lGJ2KWHtkCTR9hsdxPWOpp20xPplKw367NUaZL-anhAijwbKQ69ymOHvWA8BPaMQJOIEQp7VppPFirTW3DapF4GfIFjhJGfKEgNoz5n_xPvuT4HN5XK6ND_sxdDeemhcTl1EtPbG5QRxI9Xs5Nn7J-rIjdKOYVBZQhWd3PQOOk_KNgltetY-8mEuvKPgNhZ2yZJVuUK5jA2uGyUiIeFGmDlLLJ1QIg2M0tOZIdMVE0y4Z8e7bykIDM1sedCp9hgwmd2lsQ3io_q5adwqvg1jTki3d32cO7Cpk3cmo0zAYJTTv1K2pyYPvnTJRMkDG3GdV247-MKfjEgFclIJ7BqYaALKzsjKbumkPzKlT5NYpIDhPqPcY03deWGU3XusM0wGMF19uuoP9W1pIaBsqG7kvSJq0i__axUa3-cqrzdXOj9SG1Pyx6HwUBEdYanRohq9V1Nwhymz4guFgm0Hk4jg0yOpt3a-5NH0lId3VZMKp2bzcqaj35I35WRPKQeHnmwVvqs-CaRVRjfmi3KciRppSH8guQKK9ZrnOu84VbM3FW7bM2EOwFEsMrS6ZShR-GE2Lp5QZe_3ZV-_66DXV7Qbj&amp;t=AQJxtLreSDKkEAVK" width="540" height="720" scrolling="yes" ></iframe>'
        }
      ];
      const scrollRegex = /scrolling="(.*?)"/gm;
      const heightRegex = /height="(.*?)"/gm;
      const scrollReplaceRegex = 'scrolling="no" id="preview-iframe"';

      //Sets scrolling to no in the response
      let iframesResponse;
      this.previewData = [];
      iframesResponse = response.map(fOb => {
        // fOb.body = fOb.body.replace(scrollRegex, scrollReplaceRegex);
        // let height = fOb.body.match(heightRegex)[0].substring(8, 11);
        // let offset = parseInt(height) * 0.044;
        // height = parseInt(height) + offset;
        // let newHeight = `height="${height}"`;
        //fOb.body = fOb.body.replace(heightRegex, newHeight);

        return fOb.body;
      });
      this.iframes = iframesResponse;
    }
  }
};
</script>

<style type="text/css">
#card-parent-2 {
  position: relative;
}
.preview-card {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
