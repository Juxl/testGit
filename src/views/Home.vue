<template>
    <div class="home">
        <div id="map" ref="map" style="width: 500px;height: 500px;"></div>
    </div>
</template>

<script>
    // @ is an alias to /src
    import HelloWorld from '@/components/HelloWorld.vue'

    export default {
        name: 'home',
        data() {
            return {
                map: {}, // 地图实列
                mapArr: [] // 需要添加的点集合
            }
        },
        mounted() {
            this.map = new BMap.Map(this.$refs.map,{

            }) //创建地图
            this.map.centerAndZoom(new BMap.Point(116, 39), 11)  // 初始化地图 并设置中心点
            this.map.addControl(new BMap.MapTypeControl({
                mapTypes: [
                    BMAP_NORMAL_MAP,
                    BMAP_HYBRID_MAP
                ]
            }));
            // this.map.centerAndZoom("上海", 15);

            // 添加标记点函数
            let addMark =(point)=> {
                let marker = new BMap.Marker(point)
                this.map.addOverlay(marker)
            }

            var bounds = this.map.getBounds();
            var sw = bounds.getSouthWest();
            var ne = bounds.getNorthEast();
            var lngSpan = Math.abs(sw.lng - ne.lng);
            var latSpan = Math.abs(ne.lat - sw.lat);
            for (var i = 0; i < 5; i ++) {
                var point = new BMap.Point(sw.lng + lngSpan * (Math.random() * 0.7), ne.lat - latSpan * (Math.random() * 0.7));
                addMark(point);
            }
        },
        components: {
            HelloWorld
        }
    }
</script>
