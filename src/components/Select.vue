<template>

    <div class="select">
        <!-- 省 -->
        <div class="reault">
            <div class="reault-msg">{{ provinceReault }}</div>
            <div class="image" @click="showList(1)">
                <img src="../assets/down.png" v-if="!isProvinceList">
                <img src="../assets/up.png" v-else>
            </div>
            <div>省</div>
            <div class="area" v-show="isProvinceList">
                <div class="option" v-for="(item,index) in provinceList" :key="item.id" :class="{isSelect:item.isSelect}" @click="selectOption(1,item)">{{ item.area }}</div>
            </div>
        </div>
        <!-- 市 -->
        <div class="reault">
            <div class="reault-msg">{{ cityReault }}</div>
            <div class="image" @click="showList(2)">
                <img src="../assets/down.png" v-if="!isCityList">
                <img src="../assets/up.png" v-else>
            </div>
            <div>市</div>
            <div class="area" v-show="isCityList">
                <div class="option" v-for="(item,index) in cityList" :key="item.id" :class="{isSelect:item.isSelect}" @click="selectOption(2,item)">{{ item.area }}</div>
            </div>
        </div>
        <!-- 区 -->
        <div class="reault">
            <div class="reault-msg">{{ districtReault }}</div>
            <div class="image" @click="showList(3)">
                <img src="../assets/down.png" v-if="!isDistrictList">
                <img src="../assets/up.png" v-else>
            </div>
            <div>区/县</div>
            <div class="area" v-show="isDistrictList">
                <div class="option" v-for="(item,index) in districtList" :key="item.id" :class="{isSelect:item.isSelect}" @click="selectOption(3,item)">{{ item.area }}</div>
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
                    this.provinceReault = item.area;
                    this.$emit('codeProvinceReault', item.code)
                } else if (type == 2) {
                    this.cityList.forEach(val => {
                        val.isSelect = false;
                    })
                    item.isSelect = true;
                    this.cityReault = item.area;
                    this.$emit('codeCityReault', item.code)
                } else {
                    this.districtList.forEach(val => {
                        val.isSelect = false;
                    })
                    item.isSelect = true;
                    this.districtReault = item.area;
                    this.$emit('codeDistrictReault', item.code)
                }
                this._showAllList()
            },
            showList(type) {
                if (type == 1) {
                    this.isProvinceList = !this.isProvinceList
                    this.isCityList = false
                    this.isDistrictList = false

                } else if (type == 2) {
                    this.isCityList = !this.isCityList
                    this.isProvinceList = false
                    this.isDistrictList = false
                } else {
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
            this.provinceReault = this.province.area || this.province;
            this.cityReault = this.city.area || this.city;
            this.districtReault = this.district.area || this.district;

            this._setIsSelect(this.provinceList, this.provinceReault)
            this._setIsSelect(this.cityList, this.cityReault)
            this._setIsSelect(this.districtList, this.districtReault)
        }
    }

</script>

<style scoped>
    .select {
        display: flex;
    }

    .reault {
        position: relative;
        width: 140px;
        height: 30px;
        line-height: 30px;
        background-color: lightblue;
        display: flex;
        justify-content: space-around;
        color: #666;
    }

    img {
        width: 20px;
        vertical-align: middle;
    }

    .reault-msg {
        font-size: 16px;
        width: 80px;
        overflow: hidden;
        text-align: center;
    }

    .area {
        width: 120px;
        max-height: 180px;
        overflow: hidden;
        background-color: lightcyan;
        position: absolute;
        top: 30px;
        left: 0;
    }

    .option {
        height: 30px;
        line-height: 30px;
        text-align: center;
    }

    .isSelect {
        background-color: pink;
    }

</style>
