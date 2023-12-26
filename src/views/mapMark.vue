<template>
    <div id="container">
        <div class="" style="position: absolute;"></div>
    </div>
</template>

<script setup lang="ts">
import AMapLoader from '@amap/amap-jsapi-loader';
import img from '../assets/map.jpg'
import markData from './marks.json'

let map: any
const initMap = async () => {
    AMapLoader.load({
        key: "0ea7e0b5d7a1c4657b75d1ee64e54b66",
        version: "2.0",       // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins: [],
    }).then((AMap: any) => {
        //图片图层
        var imageLayer = new AMap.ImageLayer({
            url: img,
            // opacity:0.5,
            bounds: new AMap.Bounds(
                [114.53434, 36.38135], //左下角
                [114.601, 36.412992], //右上角
            )
        });
        //初始化地图
        map = new AMap.Map('container', {
            // center: [114.565896, 36.394500],//原始
            center: [114.569, 36.397600],
            zooms: [15.1, 20],
            // rotation: 0,
            showBuildingBlock: false,
            showLabel: false,
            // mapStyle: "amap://styles/darkblue",
            layers: [
                AMap.createDefaultLayer(),
                imageLayer,
            ]
        });

        // 设置地图显示范围
        const bounds = new AMap.Bounds([114.538368,36.385835], [114.599592,36.409556]);
        map.setLimitBounds(bounds);
        map.on('click', (e) => {
            console.log(e.lnglat.getLng(), e.lnglat.getLat());
            alert(e.lnglat.getLng() + ',' + e.lnglat.getLat())
        })

        // 设置点标记
        let markers: any = []
        const initMarker = (AMap: any) => {
            for (let i = 0; i < markData.data.length; i++) {
                let lsname = markData.data[i].name
                // let content = `<div class="info-warp-youzu">
                //             <span>${lsname}</span>
                //         </div>
                //         <div class="GreenStatus13"></div>
                //         <div class='info-line-youzu'></div>
                //         <div class='info-line-youzu1'></div>`
                let content = `<div class="markBox">
                                <div class="markerTitle">${lsname}</div>
                                <div class="marker"></div>
                                <div class="markerShadow"></div>
                                <div class="markerCircle"></div>
                              </div>`
                markers[i] = new AMap.Marker({
                    content: content,  // 自定义点标记覆盖物内容
                    position: markData.data[i].position, // 基点位置
                    offset: new AMap.Pixel(-50, -46) // 相对于基点的偏移位置
                });
                map.add(markers[i])
            }
        }
        initMarker(AMap)
    }).catch((e: any) => {
        console.log(e);
    })
}

onMounted(() => {
    initMap()
})
onUnmounted(() => {
})
</script>

<style lang="less" scoped>
@import './mark.less';

#container {
    padding: 0px;
    margin: 0px;
    width: 100vw;
    height: 100vh;
}
</style>