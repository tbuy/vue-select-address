<template>

    <div class="select">
        <!-- 省 -->
        <div class="reault">
            <div class="reault-wrap" @click="showList(1)">
                <div class="reault-msg">{{ provinceReault }}</div>
                <div class="image">
                    <img src="../assets/down.png" v-if="!isProvinceList">
                    <img src="../assets/up.png" v-else>
                </div>
            </div>
            <div class="area" v-show="isProvinceList">
                <div class="option" v-for="(item,index) in provinceList" :key="item.id" :class="{isSelect:item.isSelect}" @click="selectOption(1,item)">{{ item.name }}</div>
            </div>
        </div>
        <!-- 市 -->
        <div class="reault">
            <div class="reault-wrap" @click="showList(2)">
                <div class="reault-msg" :class="{noSelect: cityList.length == 0}">{{ cityReault }}</div>
                <div class="image">
                    <img src="../assets/down.png" v-if="!isCityList">
                    <img src="../assets/up.png" v-else>
                </div>
            </div>
            <div class="area" v-show="isCityList">
                <div class="option" v-for="(item,index) in cityList" :key="item.id" :class="{isSelect:item.isSelect}" @click="selectOption(2,item)">{{ item.name }}</div>
            </div>
        </div>
        <!-- 区 -->
        <div class="reault">
            <div class="reault-wrap" style="width: 220px" @click="showList(3)">
                <div class="reault-msg" style="width: 160px" :class="{noSelect: districtList.length == 0}">{{ districtReault }}</div>
                <div class="image">
                    <img src="../assets/down.png" v-if="!isDistrictList">
                    <img src="../assets/up.png" v-else>
                </div>
            </div>
            <div class="area" v-show="isDistrictList" style="width: 220px">
                <div class="option" v-for="(item,index) in districtList" :key="item.id" :class="{isSelect:item.isSelect}" @click="selectOption(3,item)">{{ item.name }}</div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            provinceList: {
                type: Array,
                default: []
            },
            cityList: {
                type: Array,
                default: []
            },
            districtList: {
                type: Array,
                default: []
            },
            province: {
                type: [Object, String],
                required: true
            },
            city: {
                type: [Object, String],
                required: true
            },
            district: {
                type: [Object, String],
                required: true
            },
        },
        data() {
            return {
                isProvinceList: false,
                isCityList: false,
                isDistrictList: false,
                provinceReault: '',
                cityReault: '',
                districtReault: '',
            }
        },
        methods: {
            selectOption(type, item) {
                if (type == 1) {
                    this.provinceList.forEach(val => {
                        val.isSelect = false;
                    })
                    item.isSelect = true;
                    this.provinceReault = item.name;
                    this.$emit('codeProvinceReault', item)

                    //重新选择省份 市区清空 状态清空
                    this.cityReault = '请选择';
                    this.districtReault = '请选择';
                    this.districtList.length = 0;
                    this.$emit('codeDistrictReault', 0)
                } else if (type == 2) {
                    this.cityList.forEach(val => {
                        val.isSelect = false;
                    })
                    item.isSelect = true;
                    this.cityReault = item.name;
                    this.$emit('codeCityReault', item)

                    //重新选择城市 地区清空 状态清空
                    this.districtReault = '请选择';
                    this.$emit('codeDistrictReault', 0)
                } else {
                    this.districtList.forEach(val => {
                        val.isSelect = false;
                    })
                    item.isSelect = true;
                    this.districtReault = item.name;
                    this.$emit('codeDistrictReault', item)
                }
                this._showAllList()
            },
            showList(type) {
                if (type == 1) {
                    this.isProvinceList = !this.isProvinceList
                    this.isCityList = false
                    this.isDistrictList = false

                } else if (type == 2 && this.provinceReault != '请选择') {
                    this.isCityList = !this.isCityList
                    this.isProvinceList = false
                    this.isDistrictList = false
                } else if (type == 3 && this.provinceReault != '请选择' && this.cityReault != '请选择') {
                    this.isDistrictList = !this.isDistrictList
                    this.isProvinceList = false
                    this.isCityList = false
                }

            },
            _showAllList() {
                this.isProvinceList = false
                this.isCityList = false
                this.isDistrictList = false
            },
            _setIsSelect(arr, data) {
                arr.forEach(item => {
                    this.$set(item, 'isSelect', false)
                    if (data && item.code == data.code) {
                        item.isSelect = true;
                    }
                })
            }
        },
        mounted() {
            this.provinceReault = this.province.name || this.province;
            this.cityReault = this.city.name || this.city;
            this.districtReault = this.district.name || this.district;

            this._setIsSelect(this.provinceList, this.province)
            this._setIsSelect(this.cityList, this.city)
            this._setIsSelect(this.districtList, this.district)
        }
    }

</script>

<style scoped>
    .select {
        display: flex;
    }

    .reault {
        position: relative;
        display: flex;
        justify-content: space-around;
        color: #666;
        font-size: 16px;
        margin-left: 10px;
    }

    img {
        width: 16px;
        vertical-align: middle;
    }

    .reault-wrap {
        display: flex;
        justify-content: space-around;
        border: 1px solid #ccc;
        width: 160px;
        height: 40px;
        line-height: 40px;
        border-radius: 6px;
    }

    .reault-name {
        height: 40px;
        line-height: 40px;
        margin-left: 10px;

    }

    .reault-msg {
        width: 100px;
        overflow: hidden !important;
    }



    .area {
        width: 160px;
        font-size: 16px;
        max-height: 200px;
        overflow: auto;
        background-color: #fff;
        border: 1px solid #ccc;
        border-radius: 6px;
        position: absolute;
        z-index: 999;
        top: 44px;
        left: 0;
    }

    .option {
        height: 40px;
        line-height: 40px;
        padding: 0 10px;
        box-sizing: border-box;
    }

    .isSelect {
        background-color: #E6E9EF;
        color: #FE5478;
    }

    .noSelect {
        color: #ccc;
    }

</style>
