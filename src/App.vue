<template>
    <div class="selectAddress">
        <Select :provinceList="provinceList" :cityList="cityList" :districtList="districtList" :province="province" :city="city"
            :district="district" @codeProvinceReault="codeProvinceReault" @codeCityReault="codeCityReault" @codeDistrictReault="codeDistrictReault"></Select>
    </div>
</template>

<script>
    import Select from './components/Select.vue'
    export default {
        components: {
            Select,
        },
        data() {
            return {
                //显示的地址（省/市/区）
                province: '请选择',
                city: '请选择',
                district: '请选择',
                //地址列表（省/市/区）
                provinceList: [{
                    code: 1,
                    name: '辽宁'
                }, {
                    code: 2,
                    name: '北京'
                }, {
                    code: 3,
                    name: '上海'
                }, {
                    code: 4,
                    name: '广州'
                }],
                cityList: [],
                districtList: [],

                //地址编码
                codeProvince: 0,
                codeCity: 0,
                codeDistrict: 0,
            }
        },
        methods: {
            codeProvinceReault(item) {
                this.codeProvince = item.code;
                this.province = item.name;
                if (item.code == 1) {
                    this.cityList = [{
                        code: 11,
                        name: '沈阳'
                    }, {
                        code: 12,
                        name: '抚顺'
                    }, {
                        code: 13,
                        name: '大连'
                    }, ]
                } else if (item.code == 2) {
                    this.cityList = [{
                        code: 21,
                        name: '海淀区'
                    }, ]
                } else if (item.code == 3) {
                    this.cityList = [{
                        code: 31,
                        name: '11'
                    }, {
                        code: 32,
                        name: '22'
                    }, {
                        code: 34,
                        name: '33'
                    }, ]
                } else {
                    this.cityList = [{
                        code: 31,
                        name: '11'
                    }, {
                        code: 32,
                        name: '22'
                    }, {
                        code: 34,
                        name: '33'
                    }, ]
                }
            },
            codeCityReault(item) {
                this.codeCity = item.code;
                this.city = item.name;
                this.districtList = [{
                    code: 223,
                    name: 'eeee'
                },{
                    code: 553,
                    name: 'kk'
                },{
                    code: 3123,
                    name: 'yy'
                },{
                    code: 24214,
                    name: 'gg'
                },{
                    code: 134,
                    name: 'rrr'
                }]

            },
            codeDistrictReault(item) {
                if (typeof (item) == 'number') {
                    this.codeDistrict = 0;
                } else {
                    this.district = item.name;
                    this.codeDistrict = item.code;
                }
            },
        },
    }

</script>
