<template>
    <div class="window-width" style="top: 0">
        <div    class="	">
            <h1 class="Title">Online Video Downloader
            </h1>
            <div class=" row">
                <input  v-model="youtubeURL" @keydown.enter="getInfo()" type="text" id="input" class=" col-sm-10 col-md-10 col-lg-10" placeholder="">
          <q-btn align="right" class="btn-fixed-width " style=" margin:  -1px 10px -1px 0px;" @click="getInfo()" color="primary" label="Download"></q-btn>
            </div>
            <div style="margin-top: 40px;" v-if="showResult && Object.keys(result).length >= 1">
                <h3 class="Title">Result
                </h3>
                <download-result :result="result"></download-result>
            </div>
        </div>

    </div>
</template>

<script lang="vue">
import axios from 'axios';
import DownloadResult from './DownloadResult';
export default {
    name: 'download',
    components: {
        'download-result': DownloadResult
    },
    //mounted() {},
    data() {
        return {
            youtubeURL: 'https://www.youtube.com/watch?v=hq7mUsU8ASY',
            result: [],
            showResult: false
        }
    },
    methods: {
        getInfo() {
            this.$q.loading.show({
  delay: 400 // ms
})

            var url = this.youtubeURL
            this.showResult = true
            axios.get('https://devtube-api.devswebdev.com/api/download-info', {
                    params: {
                        url: url
                    }
                })
                .then((response) => {
                    console.log(response);
                    this.result = Object.assign({}, response.data)

this.$q.loading.hide()
                })
                .catch((error) => {
                    console.log(error);

this.$q.loading.hide()
                });

        }
    }


}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Dosis');
:root {
    /* generic */
    --gutterSm: 0.4rem;
    --gutterMd: 0.8rem;
    --gutterLg: 1.6rem;
    --gutterXl: 2.4rem;
    --gutterXx: 7.2rem; // --colorPrimary400: #7e57c2;
    // --colorPrimary600: #5e35b1;
    // --colorPrimary800: #4527a0;
    --fontFamily: "Dosis", sans-serif;
    --fontSizeSm: 1.2rem;
    --fontSizeMd: 1.6rem;
    --fontSizeLg: 2.1rem;
    --fontSizeXl: 2.8rem;
    --fontSizeXx: 3.6rem;
    --lineHeightSm: 1.1;
    --lineHeightMd: 1.8;
    --transitionDuration: 300ms;
    --transitionTF: cubic-bezier(0.645, 0.045, 0.355, 1);
    /* floated labels */
    --inputPaddingV: var(--gutterMd);
    --inputPaddingH: var(--gutterLg);
    --inputFontSize: var(--fontSizeLg);
    --inputLineHeight: var(--lineHeightMd);
    --labelScaleFactor: 0.8;
    --labelDefaultPosY: 50%;
    --labelTransformedPosY: calc( (var(--labelDefaultPosY)) - (var(--inputPaddingV) * var(--labelScaleFactor)) - (var(--inputFontSize) * var(--inputLineHeight)));
    --inputTransitionDuration: var(--transitionDuration);
    --inputTransitionTF: var(--transitionTF);
}

*,
*::before,
*::after {
    box-sizing: border-box;
}

html {
    font-size: 10px;
}

body {
        top: 0;

    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    width: 100%; // height: 100vh;
    color: #455A64;
    background-color: #44484c;
    font-family: var(--fontFamily);
    font-size: var(--fontSizeMd);
    line-height: var(--lineHeightMd);
}

.Wrapper {
    top: 0;
    flex: 0 0 0%;
    max-width: 100%;
}

.Title {
    // margin: 0 0 var(--gutterXx) 0;
    padding: 0;
    color: #fff;
    font-size: var(--fontSizeXx);
    font-weight: 400;
    line-height: var(--lineHeightSm);
    text-align: center;
    text-shadow: -0.1rem 0.1rem 0.2rem var(--colorPrimary800);
}

.Input {
    position: relative;
}

.Input-text {
    display: block;
    margin: 0;
    padding: var(--inputPaddingV) var(--inputPaddingH);
    color: inherit;
    width: 1000px;
    font-family: inherit;
    font-size: var(--inputFontSize);
    font-weight: inherit;
    line-height: var(--inputLineHeight);
    border: none;
    border-radius: 0.4rem;
    transition: box-shadow var(--transitionDuration);
}

.Input-text::placeholder {
    color: #B0BEC5;
}

.Input-text:focus {
    outline: none;
    box-shadow: 0.2rem 0.8rem 1.6rem var(--colorPrimary600);
}

.Input-label {
    display: block;
    position: absolute;
    // bottom: 50%;
    left: 1rem;
    color: #fff;
    font-family: inherit;
    font-size: var(--inputFontSize);
    font-weight: inherit;
    line-height: var(--inputLineHeight);
    opacity: 0;
    transform: translate3d(0, var(--labelDefaultPosY), 0) scale(1);
    transform-origin: 0 0;
    transition: opacity var(--inputTransitionDuration) var(--inputTransitionTF), transform var(--inputTransitionDuration) var(--inputTransitionTF), visibility 0ms var(--inputTransitionDuration) var(--inputTransitionTF), z-index 0ms var(--inputTransitionDuration) var(--inputTransitionTF);
}

.Input-text:placeholder-shown+.Input-label {
    visibility: hidden;
    z-index: -1;
}

.Input-text:not(:placeholder-shown)+.Input-label,
.Input-text:focus:not(:placeholder-shown)+.Input-label {
    visibility: visible;
    z-index: 1;
    opacity: 1;
    transform: translate3d(0, var(--labelTransformedPosY), 0) scale(var(--labelScaleFactor));
    transition: transform var(--inputTransitionDuration), visibility 0ms, z-index 0ms;
}
</style>