<template>
  <div class="fff" :class="{ flcl: !clicolor.toString() }" :style="`background-color: ${getcolor}`">
    <div class="leftb">
      <sy v-for="arrs in arr" :arrs="arrs" @click="clibox(arrs)" />
    </div>
    <div class="aaa" style="min-width: 500px;">
      <dy :clicolor="clicolor" />      
    </div>
  </div>
</template>

<script>
import Dy from '../views/dynamic.vue'
import Sy from '../views/cylindrical.vue'
import { reactive, watch } from 'vue'

export default { 
  name: 'HelloWorld',
  data() {
    return {
      arr: [
        {value: [35, 94, 77, 53], val: [92, 34, 35], v: '#5c2223', c: '暗玉紫', c2: 'anyuzi'},
        {value: [0, 49, 27, 0], val: [238, 162, 164], v: '#eea2a4', c: '牡丹粉红', c2: 'mudanfenhong'},
        {value: [35, 100, 85, 54], val: [90, 25, 27], v: '#5a191b', c: '栗紫', c2: 'lizi'},
        {value: [0, 65, 38, 0], val: [240, 124, 130], v: '#f07c82', c: '香叶红', c2: 'xiangyehong'},
        {value: [35, 100, 80, 54], val: [90, 18, 22], v: '#5a1216', c: '葡萄酱紫', c2: 'putaojiangzi'},
        {value: [0, 77, 49, 0], val: [239, 90, 101], v: '#ed5a65', c: '艳红', c2: 'yanhong'},
        {value: [13, 83, 62, 3], val: [192, 72, 81], v: '#c04851', c: '玉红', c2: 'yuhong'},

                {value: [0, 84, 60, 0], val: [238, 63, 77], v: '#6e3738', c: '茶花红', c2: 'chahuahong'},
        {value: [11, 93, 77, 2], val: [192, 44, 56], v: '#6e4141', c: '高粱红', c2: 'gaolianghong'},
        {value: [22, 76, 54, 12], val: [167, 83, 90], v: '#6a4f4d', c: '满江红', c2: 'manjianghong'},
        {value: [5, 38, 20, 0], val: [227, 180, 184], v: '#e3b4b8', c: '鼠鼻红', c2: 'shubihong'},
        {value: [5, 50, 23, 0], val: [240, 161, 168], v: '#f0a1a8', c: '合欢红', c2: 'hehuanhong'},
        {value: [0, 56, 27, 0], val: [241, 147, 156], v: '#f1939c', c: '春江红', c2: 'chunjianghong'},
        {value: [19, 99, 86, 11], val: [166, 27, 41], v: '#a61b29', c: '苋菜红', c2: 'xiancaihong'},

        {value: [29, 73, 51, 28], val: [137, 78, 84], v: '#894e54', c: '烟红', c2: 'yanhong'},
        {value: [13, 76, 50, 2], val: [196, 90, 101], v: '#c45a65', c: '莓红', c2: 'meihong'},
        {value: [1, 95, 82, 0], val: [209, 26, 45], v: '#d11a2d', c: '鹅冠红', c2: 'eguanhong'},
        {value: [10, 96, 82, 2], val: [194, 31, 48], v: '#c21f30', c: '枫叶红', c2: 'fengyehong'},
        {value: [0, 93, 76, 0], val: [222, 28, 49], v: '#de1c31', c: '唐菖蒲红', c2: 'tangchangpuhong'},
        {value: [28, 100, 86, 33], val: [124, 24, 35], v: '#7c1823', c: '枣红', c2: 'zaohong'},
        {value: [36, 95, 71, 59], val: [84, 30, 36], v: '#541e24', c: '猪肝紫', c2: 'zhuganzi'},

        {value: [39, 92, 67, 64], val: [76, 31, 36], v: '#4c1f24', c: '葡萄紫', c2: 'putaozi'},
        {value: [27, 100, 79, 30], val: [130, 32, 43], v: '#82202b', c: '暗紫苑红', c2: 'anziyuanhong'},
        {value: [27, 100, 90,29], val: [130, 17, 31], v: '#82111f', c: '殷红', c2: 'yinhong'},
        {value: [0, 82, 50, 0], val: [239, 71, 93], v: '#ef475d', c: '草茉莉红', c2: 'caomolihong'},
        {value: [39, 100, 79, 63], val: [77, 16, 24], v: '#4d1018', c: '酱紫', c2: 'jiangzi'},
        {value: [0, 78, 44, 0], val: [237, 85, 106], v: '#ed556a', c: '山茶红', c2: 'shanchahong'},
        {value: [48, 45, 40, 26], val: [122, 115, 116], v: '#7a7374', c: '锌灰', c2: 'xinhui'},

        {value: [0, 86, 55, 0], val: [240, 55, 82], v: '#f03752', c: '海棠红', c2: 'haitanghong'},
        {value: [8, 22, 12, 0], val: [230, 210, 213], v: '#e6d2d5', c: '蓟粉红', c2: 'jifenhong'},
        {value: [0, 30, 12, 0], val: [240, 201, 207], v: '#f0c9cf', c: '石蕊红', c2: 'shiruihong'},
        {value: [0, 89, 62, 0], val: [238, 39, 70], v: '#ee2746', c: '淡曙红', c2: 'danshuhong'},
        {value: [56, 88, 62, 84], val: [43, 18, 22], v: '#2b1216', c: '李紫', c2: 'lizi'},        
        {value: [0, 78, 44, 0], val: [237, 85, 106], v: '#ee4863', c: '石竹红', c2: 'shizhuhong'},
        {value: [0, 65, 29, 0], val: [231, 124, 142], v: '#e77c8e', c: '淡茜红', c2: 'danqianhong'},
        
        {value: [38, 100, 81, 61], val: [80, 10, 22], v: '#500a16', c: '金鱼紫', c2: 'jinyuzi'},
        {value: [16, 61, 34, 4], val: [194, 124, 4], v: '#c27c88', c: '山黎豆红', c2: 'shanlidouhong'},
        {value: [41, 64, 44, 36], val: [115, 87, 92], v: '#73575c', c: '鼠背灰', c2: 'shubeihui'},
        {value: [0, 82, 44, 0], val: [238, 72, 102], v: '#ee4866', c: '淡蕊香红', c2: 'danruixianghong'},
        {value: [33, 100, 75, 49], val: [98, 22, 36], v: '#621624', c: '甘蔗紫', c2: 'ganzhehong'},
        {value: [8, 78, 35, 1], val: [206, 87, 109], v: '#ce5777', c: '月季红', c2: 'yuejihong'},
        {value: [5,96, 73, 1], val: [204, 22, 58], v: '#cc163a', c: '尖晶玉红', c2: 'jianjinyuhong'},

        {value: [0, 33, 11, 0], val: [241, 196, 205], v: '#f1c4cd', c: '水红', c2: 'shuihong'},
        {value: [0, 39, 14, 0], val: [238, 184, 195], v: '#eeb8c3', c: '姜红', c2: 'jianghong'},
        {value: [39, 53, 38, 25], val: [133, 109, 114], v: '#856d72', c: '芦灰', c2: 'luhui'},
        {value: [58, 90, 63, 83], val: [45, 12, 19], v: '#2d0c13', c: '茄皮紫', c2: 'qiepizi'},
        {value: [57, 72, 54, 74], val: [54, 40, 43], v: '#36282b', c: '苍蝇灰', c2: 'cangyinghui'},
        {value: [13, 90, 56, 3], val: [191, 53, 83], v: '#bf3553', c: '锦葵红', c2: 'jinkuihong'},
        {value: [0, 52, 18, 0], val: [236, 155, 173], v: '#ec9bad', c: '粉团花红', c2: 'fentuanhuahong'},

        {value: [32, 100, 84, 49], val: [99, 7, 28], v: '#63071c', c: '石竹紫', c2: 'shizhuzi'},
        {value: [52, 88, 58, 81], val: [48, 22, 28], v: '#30161c', c: '卵石紫', c2: 'luanshizi'},
        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#eea6b7', c: '晶红', c2: 'jinghong'},
        {value: [3, 26, 10, 0], val: [233, 204, 211], v: '#e9ccd3', c: '芝兰紫', c2: 'zhilanzi'},
        {value: [0, 50, 16, 0], val: [235, 160, 179], v: '#eba0b3', c: '芍药耕红', c2: 'shaoyaogenghong'},
        {value: [49, 71, 49, 58], val: [79, 56, 62], v: '#4f383e', c: '暮云灰', c2: 'muyunhui'},
        {value: [0, 52, 15, 0], val: [237, 157, 178], v: '#ed9db2', c: '豇豆红', c2: 'jiangdouhong'},

        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#ec8aa4', c: '报春红', c2: 'baochunhong'},
        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#ec7696', c: '淡绛红', c2: 'danjianghong'},
        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#ea7293', c: '凤仙花红', c2: 'fengxianhuahong'},
        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#ef82a0', c: '霞光红', c2: 'xiaguanghong'},
        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#ec2c64', c: '喜蛋红', c2: 'xidanhong'},
        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#eb507e', c: '夹竹桃红', c2: 'jiazhutaohong'},
        {value: [0, 48, 15, 0], val: [238, 166, 183], v: '#eb3c70', c: '松叶牡丹红', c2: 'songyemudanhong'},

        {value: [0, 80, 27, 0], val: [234,81, 127], v: '#ea517f', c: '莲瓣红', c2: 'lianbanhong'},
        {value: [2, 66,22, 0], val: [222, 120, 0], v: '#de7897', c: '白芨红', c2: 'baijihong'},
        {value: [26, 43, 26, 6], val: [181, 152, 161], v: '#b598a1', c: '隐红灰', c2: 'yinhonghui'},
        {value: [0, 88, 36, 0], val: [237, 47, 106], v: '#ed2f6a', c: '榲桲红', c2: 'wenpohong'},
        {value: [15, 68, 28, 2], val: [197, 112, 139], v: '#c5708b', c: '炸酱草红', c2: 'zhajiangcaohong'},
        {value: [50, 91, 54, 79], val: [51, 20, 30], v: '#33141e', c: '火鹅紫', c2: 'huoezi'},
        {value: [34, 97, 54, 50], val: [98, 29, 52], v: '#621d34', c: '鹅冠紫', c2: 'eguanzi'},

        {value: [0, 86, 30, 0], val: [239, 52, 115], v: '#ef3473', c: '品红', c2: 'pinhong'},
        {value: [53, 81, 50, 74], val: [56, 33, 41], v: '#382129', c: '磨石紫', c2: 'moshizi'},
        {value: [53, 92, 55, 81], val: [49, 15, 27], v: '#310f1b', c: '墨紫', c2: 'mozi'},
        {value: [48, 90, 50, 76], val: [56, 25, 36], v: '#381924', c: '檀紫', c2: 'tanzi'},
        {value: [0, 71, 18, 0], val: [225, 108, 150], v: '#e16c96', c: '初荷红', c2: 'chuhehong'},
        {value: [24, 99, 52, 19], val: [149, 28, 72], v: '#951c48', c: '菜头紫', c2: 'caitouzi'},
        {value: [33, 100, 58, 60], val: [98, 16, 46], v: '#62102e', c: '葡糖酒红', c2: 'putaojiuhong'},

        {value: [10, 27, 11, 0], val: [224, 200, 209], v: '#e0c8d1', c: '淡青紫', c2: 'danqingzi'},
        {value: [5, 87, 30, 1], val: [209, 60, 116], v: '#d13c74', c: '菠根红', c2: 'bogenhong'},
        {value: [40, 92, 47, 64], val: [75, 30, 47], v: '#4b1e2f', c: '海象紫', c2: 'haixiangzi'},
        {value: [0, 81, 18, 0], val: [236, 78, 138], v: '#ec4e8a', c: '兔眼红', c2: 'tuyanhong'},
        {value: [0, 85, 24, 0], val: [222, 63, 124], v: '#de3f7c', c: '嫩姜红', c2: 'nenjianghong'},
        {value: [22, 83, 34, 11], val: [168, 69, 107], v: '#a8456b', c: '洋葱紫', c2: 'yangcongzi'},
        {value: [0, 76, 16, 0], val: [206, 94, 138], v: '#ce5e8a', c: '吊钟花红', c2: 'diaozhonghuahong'},

        {value: [41, 97, 49, 68], val: [70, 22, 41], v: '#461629', c: '绀紫', c2: 'ganzi'},
        {value: [0, 87, 24, 0], val: [238, 44, 121], v: '#ee2c79', c: '紫荆红', c2: 'zijinghong'},
        {value: [0, 82, 16, 0], val: [239, 73, 139], v: '#ef498b', c: '扁豆花红', c2: 'biandouhuahong'},
        {value: [6, 13, 7, 0], val: [237, 227, 231], v: '#ede3e7', c: '马鞭草紫', c2: 'mabiancaozi'},
        {value: [0, 88, 23, 0], val: [236, 45, 122], v: '#ec2d7a', c: '藏花红', c2: 'zanghuahong'},
        {value: [49, 82, 46, 63], val: [72, 41, 54], v: '#482936', c: '斑鸠灰', c2: 'banjiuhui'},
        {value: [42, 99, 51, 69], val: [68, 14, 37], v: '#440e25', c: '古铜紫', c2: 'gutongzi'},

        {value: [7, 79, 18, 0], val: [210, 86, 140], v: '#d2568c', c: '丹紫红', c2: 'danzihong'},
        {value: [7, 20, 8, 0], val: [233, 215, 223], v: '#e9d7df', c: '丁香淡紫', c2: 'dingxiangzi'},
        {value: [4, 89, 21, 0], val: [210, 53, 125], v: '#d2357d', c: '玫瑰红', c2: 'meiguihong'},
        {value: [63, 74, 52, 70], val: [54, 41, 47], v: '#36292f', c: '古鼎灰', c2: 'gudingzi'},
        {value: [10, 67, 12, 0], val: [210, 118, 163], v: '#d276a3', c: '菱锰红', c2: 'lingmenghong'},
        {value: [19, 68, 18, 1], val: [192, 111, 152], v: '#c06f98', c: '樱花紫', c2: 'yinghuazi'},
        {value: [11, 97, 10, 0], val: [204, 85, 149], v: '#cc5595', c: '龙须红', c2: 'longxuhong'},

        {value: [16, 79, 14, 1], val: [195, 86, 145], v: '#c35691', c: '电气石紫', c2: 'dianqishizi'},
        {value: [18, 91, 18, 2], val: [186, 47, 123], v: '#ba2f7b', c: '玫瑰紫', c2: 'meiguizi'},
        {value: [27, 97, 27, 14], val: [155, 30, 100], v: '#9b1e64', c: '苋菜紫', c2: 'xiancaizi'},
        {value: [53, 75, 41, 41], val: [93, 63, 81], v: '#5d3f51', c: '紫灰', c2: 'zihui'},
        {value: [55, 87, 41, 52], val: [78, 42, 64], v: '#4e2a40', c: '龙晴鱼紫', c2: 'lingjingyuzi'},
        {value: [24, 58, 15, 1], val: [188, 132, 168], v: '#bc84a8', c: '青蛤壳紫', c2: 'qinghakezi'},
        {value: [23, 53, 14, 1], val: [192, 142, 175], v: '#c08eaf', c: '罗兰紫', c2: 'luolanzi'},

        {value: [58, 96, 40, 61], val: [65, 28, 53], v: '#411c35', c: '荸荠紫', c2: 'biqizi'},
        {value: [31, 71, 15, 1], val: [173, 101, 152], v: '#ad6598', c: '豆蔻紫', c2: 'doukouzi'},
        {value: [35, 75, 18, 2], val: [163, 92, 143], v: '#a35c8f', c: '扁豆紫', c2: 'biandouzi'},
        {value: [49, 100, 29, 32], val: [104, 23, 82], v: '#681752', c: '牵牛紫', c2: 'qianniuzi'},
        {value: [44, 85, 24, 10], val: [137, 66, 118], v: '#894276', c: '芓紫', c2: 'zizi'},
        {value: [45, 99, 24, 16], val: [126, 32, 101], v: '#7e2065', c: '葛巾紫', c2: 'gejinzi'},
        {value: [43, 97, 19, 8], val: [139, 38, 113], v: '#8b2671', c: '青莲', c2: 'qinglian'},
      ]
    }
  },
  components: {
    Dy, Sy
  },
  setup() {
    let clicolor = reactive({value: [0, 0, 0, 0], val: [255, 255, 255], v: '#ddd', c: '中国色', c2: 'zhonguose'})
    function clibox (ar) {
      // clicolor.key = ar
      Object.assign(clicolor,ar)
    }

    return {
      clibox,
      clicolor
    }
  },
  computed: {
    getcolor: function () {
      return this.clicolor.v
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
  .leftb {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    height: 100%;
    width: 420px;
    margin-left: 180px;
  }
  .fff {
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    padding: 45px;
    transition: background-color 2s ease-in;
    display: flex;
  }
  .flcl {
    background-image: url('../img/qq.png');
  }
</style>
