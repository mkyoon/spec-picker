<template>
    <div class="twelve wide stretched column detail" style="margin: 0;">
        <div class="ui three top attached steps">
            <div class="step" :class="[ activeStep == spec[key].title ? 'active' : '']" v-for="(s, key) in spec" :key="s.id" @click.prevent="selectStep(s.title)">
                <!-- <i class="video icon"></i> -->
                <div class="content">
                    <div class="title">{{s.title}}</div>
                    <div class="description">{{s.desc}}</div>
                </div>
            </div>
            <!-- <div class="step active">
                <i class="volume up icon"></i>
                <div class="content">
                    <div class="title">Audio Spec</div>
                    <div class="description">Enter billing information</div>
                </div>
            </div>
            <div class="step">
                <i class="comment alternate icon"></i>
                <div class="content">
                    <div class="title">Subtitles</div>
                    <div class="description">Verify order details</div>
                </div>
            </div> -->
        </div>
        <div class="ui attached segment" :class="[ activeStep == spec[key].title ? 'active' : '']" v-for="(s, key) in spec" :key="s.id">
            <div class="picker">
                <div class="column radio-name" v-for="(subspec, subspeckey) in s.items" :key="subspec.id">
                    <div class="picker-title">{{subspec.title}}</div>

                    <div class="input" :class="s.inputType" v-for="(item, ikey) in subspec.items" :key="item.id">
                        <input :type="s.inputType" :id="['temp_id_' + key + subspeckey + ikey]" :name="['temp_name_' + key + subspeckey]">
                        <label :for="['temp_id_' + key + subspeckey + ikey]">{{item.title}}</label>
                    </div>
                </div>
            </div>
            <div style="text-align:right; padding:1rem 0;">
                <button class="ui right labeled icon button">
                    <i class="right arrow icon"></i>
                    Next
                </button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SpecPicker',
    data () {
        return {
            activeStep: null,
            spec: [
                {
                title: 'Video Specs',
                desc: 'Choose your video options',
                inputType: 'checkbox',
                items: [
                    {
                    title: 'Container',
                    selected: [],
                    items: [
                        { title: 'MOV' },
                        { title: 'MXF' },
                        { title: 'MPG' },
                        { title: 'WMV+H13' },
                        { title: 'MP4' },
                    ]
                    },
                    {
                    title: 'Codec',
                    selected: [],
                    items: [
                        { title: 'APPLE Prores 422 HQ' },
                        { title: 'APPLE Prores 4444' },
                        { title: 'XDCAM 422' },
                        { title: 'H.264' },
                        { title: 'MPEG-TS' },
                    ]
                    },
                    {
                    title: 'Frame Rate',
                    selected: [],
                    items: [
                        { title: '23.98psf' },
                        { title: '24p' },
                        { title: '25psf' },
                        { title: '50i' },
                        { title: '59.94i(DF)' },
                        { title: '59.94i(NDF)' },
                    ]
                    },
                    {
                    title: 'Resolution',
                    selected: [],
                    items: [
                        { title: '720*480[1.66]' },
                        { title: '720*576[1.66]' },
                        { title: '720*480[1.66ANA]' },
                        { title: '720*576[1.66ANA]' },
                        { title: '720*480[1.85LB]' },
                        { title: '720*576[1.85LB]' },
                        { title: '1280*720[1.78]' },
                        { title: '1440*1080[1.66]' },
                        { title: '1920*1080[1.78]' },
                        { title: '1920*1080[1.85LB]' },
                        { title: '1920*1080[2.35LB]' },
                        { title: '1920*1080[2.39LB]' },
                        { title: '1998*1080[1.85]' },
                        { title: '2048*858[2.39]' },
                        { title: '3840*2160[1.78]' },
                        { title: '3840*2160[1.85LB]' },
                        { title: '3840*2160[2.39LB]' },
                    ]
                    }
                ]
                },
                {
                title: 'Audio Specs',
                desc: 'Choose your audio options',
                inputType: 'checkbox',
                items: [
                    {
                    title: 'Audio Elements',
                    selected: [],
                    items: [
                        { title: '2ch' },
                        { title: '4ch' },
                        { title: '5.1ch' },
                        { title: '8ch' },
                        { title: '10ch' },
                        { title: '12ch' },
                        { title: '14ch' },
                        { title: '16ch' },
                    ]
                    },
                    {
                    title: 'Bit Depth',
                    selected: [],
                    items: [
                        { title: '24bit' },
                        { title: '48bit' },
                    ]
                    },
                    {
                    title: 'Sample Rate',
                    selected: [],
                    items: [
                        { title: '48kHz' },
                    ]
                    },
                    {
                    title: 'Original Spoken Language',
                    selected: [],
                    items: [
                        { title: 'Korean' },
                        { title: 'English' },
                        { title: 'Turkish' },
                    ]
                    },
                ]
                },
                {
                title: 'Subtitles',
                desc: 'Choose your subtitle options',
                inputType: 'checkbox',
                items: [
                    {
                    title: 'Dialogue Subtitle',
                    items: [
                        { title: 'Korean' },
                        { title: 'English' },
                        { title: 'None' },
                    ]
                    },
                    {
                    title: 'Text on screen (Burned-in informational text in Korean)',
                    items: [
                        { title: 'Korean' },
                        { title: 'English' },
                        { title: 'None' },
                    ]
                    },
                ]
                },
            ]
        }
    },
    methods: {
        selectStep(name) {
            this.activeStep = name;
        }
    },
    mounted () {
        this.activeStep = this.spec[0].title;
    }
}
</script>

<style lang="scss" scoped>
.input {
    &.checkbox,
    &.radio {
        display: inline-block;
        position: relative;
        // margin: .2rem 2rem .2rem 0;
        vertical-align: middle;
        cursor: pointer;
        label {
            display: block;
            vertical-align: middle;
            cursor: pointer;
        }
        input {
            width: 0;
            height: 0;
            overflow: hidden;
            position: absolute;
            padding: 0;
            border: 0;
            opacity: 0;
            line-height: 0;
        }
        label {
            // min-height: 2.5rem;
            margin: 0;
            // text-indent: 35px;
            font-weight: 400;
            font-size: 1.5rem;
            text-align: center;
            &:before {
                // content: '';
                display: block;
                position: absolute;
                top: 2px;
                left: 0;
                width: 25px;
                height: 25px;
                border: 0 none;
                // background: url('../images/icon_form.png') no-repeat;
                // background-position: -12px -12px;
            }
        }
        input:checked + label {
            background-color: #ccc;
            color: #f00;
            &:before {
                // background-position: -62px -12px;
            }
        }
    }
}

.picker {
    display: flex;
    align-items: stretch;
    .column {
        display: flex;
        flex: 1 1 0;
        flex-direction: column;
        margin: 0;
        > * {
            display: flex;
            flex: 1 1 auto;
            border: 1px solid #fff;
        }
        .picker-title {
            flex: none;
            height: 3em;
            text-align: center;
            line-height: 1.5;
            background-color: #d8f8d8;
            align-items: center;
            justify-content: center;
        }
        label {
            flex: 1 1 0;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: .3em;
            background-color: #eee;
        }
    }
}

.spec-list-item {
    width: 100%;
}

.accordion ul { margin-left: 2rem;}
.bookmark {color: #f00}
.detail .segment {
    display: none;
    &.active {
        display: block;
    }
}
</style>

