<template>
    <div id="app">
        <div class="select">
            <Select :provinceList="provinceList" :cityList="cityList" :districtList="districtList" :province="province" :city="city"
                :district="district" @codeProvinceReault="codeProvinceReault" @codeCityReault="codeCityReault" @codeDistrictReault="codeDistrictReault"></Select>
        </div>
        <div>
            <div>选中的省级code:{{codeProvice}}</div>
            <div>选中的市级code:{{codeCity}}</div>
            <div>选中的区及code:{{codeDistrict}}</div>
        </div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                provinceList: [{
                    code: 1,
                    area: '辽宁'
                }, {
                    code: 2,
                    area: '北京'
                }, {
                    code: 3,
                    area: '上海'
                }, {
                    code: 4,
                    area: '广州'
                }],
                cityList: [{
                    code: 11,
                    area: '沈阳'
                }, {
                    code: 12,
                    area: '大连'
                }, {
                    code: 13,
                    area: '锦州'
                }, {
                    code: 14,
                    area: '抚顺'
                }],
                districtList: [{
                    code: 21,
                    area: '大东'
                }, {
                    code: 22,
                    area: '沈河'
                }, {
                    code: 23,
                    area: '和平'
                }, {
                    code: 24,
                    area: '铁西'
                }],
                province: '请选择',
                city: '请选择',
                district: '请选择',
                codeProvice: 0,
                codeCity: 0,
                codeDistrict: 0
            }
        },
        methods: {
            codeProvinceReault(code) {
                this.codeProvice = code
            },
            codeCityReault(code) {
                this.codeCity = code
            },
            codeDistrictReault(code) {
                this.codeDistrict = code
            },
        }
    }

</script>

<style>
    * {
        margin: 0;
        padding: 0;
    }

    .select {
        display: flex;
    }

</style>
