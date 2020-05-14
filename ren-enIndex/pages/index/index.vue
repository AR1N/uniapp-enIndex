<template>
    <view class="estimate">
        <scroll-view  scroll-y="true" class="scroll-box" id="user-main" :scroll-into-view="toView" :scroll-top="scrollTop">
            <ren-enIndex ref="ren" :original="userData"></ren-enIndex>
            <view class="fixed-right">
                <view class="item-index c-flex-center" v-for="(item, index) in letters" :key="index" @click="onIndexClick(item.letter)">{{ item.letter }}</view>
            </view>
            <view class="c-btm-safearea"></view>
        </scroll-view>
    </view>
</template>

<script>
import RenEnIndex from '@/components/ren-enIndex/ren-enIndex.vue';

export default {
    components: {
        RenEnIndex
    },
    data() {
        return {
            toView: 'user-find',
            letters: [],
            userData: [
                { name: 'AREN', avatar: 'https://ftp.bmp.ovh/imgs/2020/05/81b19b3314dad88a.png' },
                { name: '艾希', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/Ashe.png' },
                { name: '小学僧', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/LeeSin.png' },
                { name: '托儿索', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/Yasuo.png' },
                { name: '放逐之刃', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/Riven.png' },
                { name: '崔斯特', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/TwistedFate.png' },
                { name: '潮汐海灵', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/Fizz.png' },
                { name: '刀锋意志', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/Irelia.png' },
                { name: '#无名', avatar: 'http://game.gtimg.cn/images/lol/act/img/champion/MasterYi.png' }
            ]
        };
    },
    onReady() {
        let data = this.$refs.ren.sortedData;
        this.letters = data.filter(item => {
            if (item.hasData) {
                return item;
            }
        });
    },
    onLoad() {},
    methods: {
        onIndexClick(index) {
            // let text = `<font  style="font-size:30px;">${index}</font>`;//app可以原生提示
            // plus.nativeUI.toast(text, {
            //     verticalAlign: 'center',
            //     type: 'richtext'
            // });
            uni.showToast({
                icon: 'none',
                title: index
            });
            if (index == '#') {
                this.toView = 'other';
            } else {
                this.toView = index;
            }
        }
    }
};
</script>

<style lang="scss" scoped>
.estimate {
    .scroll-box {
        height: 100vh;
        .title {
            margin-top: 20rpx;
            color: #5a5a5a;
            height: 94rpx;
            line-height: 94rpx;
            padding-left: 24rpx;
            font-size: 36rpx;
            font-weight: bold;
            background-color: #fff;
        }

        .fixed-right {
            position: fixed;
            top:200rpx;
            right: 10rpx;
            width: 40rpx;
            padding: 20rpx 0;
            background-color: #21191b;
            border-radius: 32rpx;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            z-index: 99;
            .item-index {
                color: #b89249;
                width: 24rpx;
                height: 24rpx;
                font-weight: bold;
                font-size: 20rpx;
                text-align: center;
                padding: 12rpx 0;
            }
        }
    }
}
</style>
