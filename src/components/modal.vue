<template>
    <div class="modal">
        <div class="modal__overlay"></div>
        <div class="modal__block">
            <h2 class="modal__title">Редактировать запись</h2>

            <div :class="{
                    'modal__hover': true,
                    'modal__hover_active': activeMap
                 }"
                 id="map"
            ></div>
            <button
                :class="{
                    'modal__button': true,
                    'modal__button_disabled': activeMap
                }"
                @click="setPolygon()"
                :disabled="activeMap"
            >Редактировать полигон</button>
            <button
                :class="{
                    'modal__button': true,
                    'modal__button_disabled': activeMap
                }"
                @click="setMark()"
                :disabled="activeMap"
            >Редактировать метку</button>
            <br/>
            <button
                :class="{
                    'modal__button': true,
                }"
                @click="savePolygon()"
                v-if="activeMap"
            >Сохранить</button>

            <div class="mBlock">

                <div class="mBlock__col6">
                    <div class="mBlock__radio">
                        <p class="mBlock__label">Статус продажи: </p>

                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__status_inSell">
                            В продаже
                            <input type="radio" name="status" id="mBlock__radio__status_inSell" class="mBlock__radio custom__input" value="В продаже" v-model="fields.status">
                            <span class=" custom__checkmark"></span>
                        </label>
                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__status_sold">
                            Продано
                            <input type="radio" name="status" id="mBlock__radio__status_sold" class="mBlock__radio custom__input" value="Продано" v-model="fields.status">
                            <span class=" custom__checkmark"></span>
                        </label>
                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__status_stop">
                            Приостановленно
                            <input type="radio" name="status" id="mBlock__radio__status_stop" class="mBlock__radio custom__input" value="Приостановленно" v-model="fields.status">
                            <span class=" custom__checkmark"></span>
                        </label>
                    </div>
                    <div class="mBlock__radio">
                        <p class="mBlock__label">ГПЗУ: </p>

                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__city_plan_yes">
                            Да
                            <input type="radio" name="city_plan" id="mBlock__radio__city_plan_yes" class="mBlock__radio custom__input" value="Да">
                            <span class=" custom__checkmark"></span>
                        </label>
                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__city_plan_no">
                            Нет
                            <input type="radio" name="city_plan" id="mBlock__radio__city_plan_no" class="mBlock__radio custom__input" value="Нет">
                            <span class=" custom__checkmark"></span>
                        </label>
                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__city_plan_soon">
                            Скоро будет
                            <input type="radio" name="city_plan" id="mBlock__radio__city_plan_soon" class="mBlock__radio custom__input" value="Скоро будет">
                            <span class=" custom__checkmark"></span>
                        </label>
                    </div>
                </div>
                <div class="mBlock__col6">
                    <div class="mBlock__radio">
                        <!--style="margin-bottom: 10px;"-->
                        <p class="mBlock__label">Назначение: </p>

                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__purpose_living">
                            Жилищная
                            <input type="radio" name="purpose" id="mBlock__radio__purpose_living" class="mBlock__radio custom__input" value="Жилищная">
                            <span class=" custom__checkmark"></span>
                        </label>
                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__purpose_trading">
                            Торговая
                            <input type="radio" name="purpose" id="mBlock__radio__purpose_trading" class="mBlock__radio custom__input" value="Торговая">
                            <span class=" custom__checkmark"></span>
                        </label>
                        <label class="mBlock__label_radio custom__radio" for="mBlock__radio__purpose_rent">
                            Арендная
                            <input type="radio" name="purpose" id="mBlock__radio__purpose_rent" class="mBlock__radio custom__input" value="Арендная">
                            <span class=" custom__checkmark"></span>
                        </label>
                    </div>
                </div>

                <div class="mBlock__col6">
                    <label class="mBlock__label" for="mBlock__input__address">Адрес</label>
                    <input type="text" id="mBlock__input__address" class="mBlock__input" v-model="fields.address" placeholder="Укажите адрес">
                    <label class="mBlock__label" for="mBlock__input__area">Округ</label>
                    <input type="text" id="mBlock__input__area" class="mBlock__input" v-model="fields.area" placeholder="Укажите округ">
                    <label class="mBlock__label" for="mBlock__input__district">Район</label>
                    <input type="text" id="mBlock__input__district" class="mBlock__input" v-model="fields.district" placeholder="Укажите район">
                    <label class="mBlock__label" for="mBlock__input__square">Площадь (кв.м)</label>
                    <input type="text" id="mBlock__input__square" class="mBlock__input" v-model="fields.square" placeholder="Укажите площадь">
                    <label class="mBlock__label" for="mBlock__input__cadastral_number">Кадастравый номер</label>
                    <input type="text" id="mBlock__input__cadastral_number" class="mBlock__input" v-model="fields.cadastral_number" placeholder="Укажите кадастровый номер">
                    <label class="mBlock__label" for="mBlock__input__exploitation_permission">Вид разрешенного использования</label>
                    <input type="text" id="mBlock__input__exploitation_permission" class="mBlock__input" v-model="fields.exploitation_permission" placeholder="Укажите вид использования">
                </div>
                <div class="mBlock__col6">

                    <label class="mBlock__label" for="mBlock__input__rights_type">Вид права</label>
                    <input type="text" id="mBlock__input__rights_type" class="mBlock__input" v-model="fields.rights_type" placeholder="Вид права">
                    <label class="mBlock__label" for="mBlock__input__surface_square">Наземная площадь</label>
                    <input type="text" id="mBlock__input__surface_square" class="mBlock__input" v-model="fields.surface_square" placeholder="Наземная площадь">
                    <label class="mBlock__label" for="mBlock__input__building_density">Плотность застройки</label>
                    <input type="text" id="mBlock__input__building_density" class="mBlock__input" v-model="fields.building_density" placeholder="Плотность застройки">
                    <label class="mBlock__label" for="mBlock__input__effective_square_index">Коэфициент для рассчёта полезной площади</label>
                    <input type="text" id="mBlock__input__effective_square_index" class="mBlock__input" v-model="fields.effective_square_index" placeholder="Коэфициент">
                    <label class="mBlock__label" for="mBlock__input__effective_square">Полезная/продаваемая площадь</label>
                    <input type="text" id="mBlock__input__effective_square" class="mBlock__input" v-model="fields.effective_square" placeholder="Полезная/продаваемая площадь">
                    <label class="mBlock__label" for="mBlock__input__price">Стоимость</label>
                    <input type="text" id="mBlock__input__price" class="mBlock__input" v-model="fields.price" placeholder="Укажите стоимость">
                </div>

                <button class="modal__button" @click="saveData">
                    <i class="mdi content-save"></i>
                    Сохранить
                </button>

                <!--<label class="mBlock__label" for="mBlock__input__coordinates">Координаты</label>-->
                <!--<input type="text" id="mBlock__input__coordinates" class="mBlock__input">-->
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Modal',
    data () {
        return {
            activeMap: false,

            fields: {
                address: null,
                area: null,
                district: null,
                cadastral_number: null,
                exploitation_permission: null,
                rights_type: null,
                surface_square: null,
                building_density: null,
                effective_square_index: null,
                effective_square: null,
                price: null,

                status: null
            },

            ymap: null,

            editingState: {
                editPolygon: false,
                editPlaceMark: false,
            },

            placeMark: null,
            newPolygon: null,
            polygonCoordinates: null,

            coordinates: [[55.798385,37.410639],[55.798563,37.4098148],[55.7983715,37.4096924],[55.7982466,37.409713],[55.7981138,37.4098607],[55.7979948,37.4103682],[55.798385,37.410639]]
        }
    },
    async mounted(){
        let polygon, polygonData;

        polygonData = this.reverseArr(this.coordinates);
        polygon = polygonData.toString().replace(/\s|\[|\]/g,"");

        document.getElementById('map').style.backgroundImage = `url('https://static-maps.yandex.ru/1.x/?size=650,250&z=16&l=map&pl=c:757979C0,f:86C678A0,w:2,${polygon}')`;
    },
    methods:{
        setPolygon(){
            this.activeMap = true;
            this.editingState.editPolygon = true;

            let temp = null;

            if(!this.newPolygon){
                temp = [[55.798385,37.410639],[55.798563,37.4098148],[55.7983715,37.4096924],[55.7982466,37.409713],[55.7981138,37.4098607],[55.7979948,37.4103682],[55.798385,37.410639]];
            }else{
                temp = this.reverseArrBack(this.newPolygon[0]);
            }

            return new Promise((resolve, reject)=> {
                ymaps.ready(()=>{
                    this.ymap = new ymaps.Map("map", {
                        center: [55.79827889999367, 37.41016569999997],
                        zoom: 17,
                        controls: []
                    });

                    let myPolygon = new ymaps.Polygon([
                        temp
                    ], {}, {
                        editorDrawingCursor: "crosshair",
                        // editorMaxPoints: 7,
                        fillColor: '#86C678',
                        strokeColor: '#757979',
                        fillOpacity: .5,
                        strokeWidth: 2
                    });

                    this.ymap.geoObjects.add(myPolygon);
                    this.ymap.state.center = myPolygon.geometry.getBounds();

                    let stateMonitor = new ymaps.Monitor(myPolygon.editor.state);
                    stateMonitor.add("drawing", function (newValue) {
                        myPolygon.options.set("strokeColor", newValue ? '#59AC46' : '#757979');
                    });

                    myPolygon.editor.startDrawing();

                    myPolygon.events.add('geometrychange', ()=>{
                        // let temp = myPolygon.geometry.getCoordinates();
                        this.newPolygon = myPolygon.geometry.getCoordinates();
                        this.polygonCoordinates = myPolygon.geometry.getBounds();
                    });
                })
            });
        },
        setMark(){
            let temp = null;

            this.activeMap = true;
            this.editingState.editPlaceMark = true;

            if(!this.newPolygon){
                temp = [[55.798385,37.410639],[55.798563,37.4098148],[55.7983715,37.4096924],[55.7982466,37.409713],[55.7981138,37.4098607],[55.7979948,37.4103682],[55.798385,37.410639]];
            }else{
                temp = this.reverseArrBack(this.newPolygon[0]);
            }

            return new Promise((resolve, reject)=> {
                ymaps.ready(()=>{
                    this.ymap = new ymaps.Map("map", {
                        center: [55.79827889999367, 37.41016569999997],
                        zoom: 17,
                        controls: []
                    });

                    let myPolygon = new ymaps.Polygon([
                        temp
                    ], {}, {
                        editorDrawingCursor: "crosshair",
                        // editorMaxPoints: 7,
                        fillColor: '#86C678',
                        strokeColor: '#757979',
                        fillOpacity: .5,
                        strokeWidth: 2
                    });

                    this.ymap.geoObjects.add(myPolygon);
                    this.ymap.state.center = myPolygon.geometry.getBounds();

                    let stateMonitor = new ymaps.Monitor(myPolygon.editor.state);
                    stateMonitor.add("drawing", function (newValue) {
                        myPolygon.options.set("strokeColor", newValue ? '#59AC46' : '#757979');
                    });

                    if(!this.placeMark){
                        this.placeMark = this.getPolyCenter(myPolygon.geometry.getBounds());
                    }

                    let myPlacemark = new ymaps.Placemark(this.placeMark, {
                        // Чтобы балун и хинт открывались на метке, необходимо задать ей определенные свойства.

                        balloonContentHeader: "Балун метки",
                        balloonContentBody: "Содержимое <em>балуна</em> метки",
                        balloonContentFooter: "Подвал",
                        hintContent: "Хинт метки"
                    },{
                        draggable: true,
                        preset: 'islands#darkGreenDotIcon',
                        iconColor: '#59AC46'
                    });

                    this.ymap.geoObjects.add(myPlacemark);

                    myPlacemark.events.add('dragend', (e)=>{
                        this.placeMark = myPlacemark.geometry.getCoordinates();
                    });
                })
            });
        },
        getPolyCenter(arr){
            let minX = arr[0][1];
            let minY = arr[0][0];
            let maxX = arr[1][1];
            let maxY = arr[1][0];

            let avgX = (minX + maxX) / 2;
            let avgY = (minY + maxY) / 2;

            return [avgY, avgX];
        },
        savePolygon(){
            let mapHover = document.getElementById('map'),
                arr, polygonCoord, implement;

            if(this.editingState.editPolygon){
                implement = new Promise((resolve, reject)=>{
                    arr = this.reverseArr(this.newPolygon, true);
                    polygonCoord = arr.toString().replace(/\s|\[|\]/g,"");
                    mapHover.style.backgroundImage = `url('https://static-maps.yandex.ru/1.x/?size=650,250&z=15&l=map&pl=c:757979C0,f:86C678A0,w:2,${polygonCoord}')`;

                    resolve(true)
                });
            }else if(this.editingState.editPlaceMark){
                implement = new Promise((resolve, reject)=>{
                    arr = this.reverseArr(this.newPolygon, true);
                    polygonCoord = arr.toString().replace(/\s|\[|\]/g,"");
                    mapHover.style.backgroundImage = `url('https://static-maps.yandex.ru/1.x/?size=650,250&z=15&l=map&pl=c:757979C0,f:86C678A0,w:2,${polygonCoord}')`;

                    resolve(true)
                });
            }

            if(implement) {
                this.activeMap = false;
                this.editingState.editPlaceMark = false;
                this.editingState.editPolygon = false;

                this.ymap.destroy();
            }
        },
        /* FUCKING MAGIC - DO NOT TOUCH */
        reverseArr(arr, newCoord = false){
            let reverse, newArr;

            if(newCoord){
                newArr = arr[0].map((el, index)=>{
                    if(el[0].toString().slice(0,1) !== '3'){
                        reverse = el.reverse();
                        return reverse;
                    }
                    return el;
                });
            }else{
                newArr = arr.map((el, index)=>{
                    if(el[0].toString().slice(0,1) !== '3'){
                        reverse = el.reverse();
                        return reverse;
                    }
                    return el;
                });
            }

            return newArr;
        },
        reverseArrBack(arr, newCoord = false){
            let reverse, newArr;

            if(newCoord){
                newArr = arr[0].map((el, index)=>{
                    if(el[0].toString().slice(0,1) !== '5'){
                        reverse = el.reverse();
                        return reverse;
                    }
                    return el;
                });
            }else{
                newArr = arr.map((el, index)=>{
                    if(el[0].toString().slice(0,1) !== '5'){
                        reverse = el.reverse();
                        return reverse;
                    }
                    return el;
                });
            }

            return newArr;
        },
        /* FUCKING MAGIC - DO NOT TOUCH end */

        saveData(){
            this.fields.placeMark = this.placeMark;
            this.fields.newPolygon = this.newPolygon;
            this.fields.polygonCoordinates = this.polygonCoordinates;
            this.$emit('save', this.fields)
        }
    },

}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Open+Sans:300,400,700&subset=cyrillic');

/* Customize the label (the container) */
.custom__radio {
    display: block;
    position: relative;
    padding-left: 30px;
    margin-bottom: 12px;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

/* Hide the browser's default radio button */
.custom__input {
    position: absolute;
    opacity: 0;
}

/* Create a custom radio button */
.custom__checkmark {
    position: absolute;
    top: 3px;
    left: 0;
    height: 14px;
    width: 14px;
    background-color: #DEDEDE;
    border-radius: 50%;
}

.custom__input:hover ~ .custom__checkmark { background-color: #ccc; }
.custom__input:checked ~ .custom__checkmark { background-color: #4EB645; }
.custom__input:checked ~ .custom__checkmark:after { display: block; }

/* Create the indicator (the dot/circle - hidden when not checked) */
.custom__checkmark:after {
    content: "";
    position: absolute;
    display: none;
}

/* Style the indicator (dot/circle) */
.custom__radio .custom__checkmark:after {
    top: 3px;
    left: 3px;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: white;
}


    .modal{
        font-family: 'Open Sans', sans-serif;
    }

    button{
        background: none;
        border: none;
        outline: none;
        font-size: 18px;
        font-weight: 400;
        font-family: 'Open Sans', sans-serif;
        cursor: pointer;
    }
    input:focus{
        outline: none;
    }
    input:focus::-webkit-input-placeholder{
        text-indent: -500px;
        transition: text-indent 0.3s ease;
    }
    input:focus:-moz-placeholder{
        text-indent: -500px;
        transition: text-indent 0.3s ease;
    }
    input:focus::-moz-placeholder{
        text-indent: -500px;
        transition: text-indent 0.3s ease;
    }
    input:focus:-ms-input-placeholder{
        text-indent: -500px;
        transition: text-indent 0.3s ease;
    }
    input::-webkit-input-placeholder{
        color: #aaacae;
        font-size: 15px;
        font-weight: 400;
        font-family: 'Open Sans', sans-serif;
        text-indent: 0px;
        transition: text-indent 0.3s ease;
    }
    input:-moz-placeholder{
        color: #aaacae;
        font-size: 15px;
        font-weight: 400;
        font-family: 'Open Sans', sans-serif;
        text-indent: 0px;
        transition: text-indent 0.3s ease;
    }
    input::-moz-placeholder{
        color: #aaacae;
        font-size: 15px;
        font-weight: 400;
        font-family: 'Open Sans', sans-serif;
        text-indent: 0px;
        transition: text-indent 0.3s ease;
    }
    input:-ms-input-placeholder{
        color: #aaacae;
        font-size: 15px;
        font-weight: 400;
        font-family: 'Open Sans', sans-serif;
        text-indent: 0px;
        transition: text-indent 0.3s ease;
    }

    .modal__button{
        /*background: aqua;*/
        color: #4EB645;
        border: 2px solid #4EB645;
        -webkit-border-radius: 7px;
        -moz-border-radius: 7px;
        border-radius: 7px;
        padding: 10px 15px;
        margin: 7px 10px;
        font-size: 16px;
        font-weight: 600;
        transition: all .3s ease-in-out;
    }
    .modal__button:hover{
        background: #4EB645;
        color: #fff;
    }
    .modal__button_disabled{
        cursor: no-drop;
        background: #EDEDED;
        color: #4EB645;
        border-color: #4EB645;
    }
    .modal__button_disabled:hover{
        background: #EDEDED;
        color: #4EB645;
        border-color: #4EB645;
    }
    .modal__block{
        display: block;
        position: absolute;
        width: 1024px;
        overflow: hidden;
        /*height: auto;*/
        top: 50px;
        left: calc(50% - 512px);
        background: #fff;
        border: 1px solid #D8D8D8;
        border-radius: 4px;
        padding: 15px 20px;
        -webkit-box-shadow: 7px 7px 10px 0px rgba(194,194,194,0.6);
        -moz-box-shadow: 7px 7px 10px 0px rgba(194,194,194,0.6);
        box-shadow: 7px 7px 10px 0px rgba(194,194,194,0.6);
        z-index: 101;
    }
    .modal__overlay{
        background: #000;
        opacity: .5;
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        z-index: 99;
    }
    .modal__title{
        color: #566270;
        padding-bottom: 7px;
        border-bottom: 2px solid #566270;
    }
    .modal__hover{
        height: 250px;
        margin: 0 -20px 20px -20px;

        background-image: url('https://loading.io/assets/img/landing/curved-bars.svg');
        background-repeat: no-repeat;
        background-position: center;
        background-size: cover;
    }
    .modal__hover_active{
        height: 450px;
    }

    .mBlock{
        width: 100%;
        height: 450px;
        box-sizing: border-box;
        overflow-y: scroll;
        position: relative;
        display: flex;
        -ms-flex-wrap: wrap;
        flex-wrap: wrap;
    }
    .mBlock__col6{
        -ms-flex: 0 0 50%;
        flex: 0 0 50%;
        max-width: 50%;
        position: relative;
        width: 100%;
        min-height: 1px;
        padding-right: 15px;
        padding-left: 15px;
        box-sizing: border-box;
    }
    .mBlock__radio{
        text-align: left;
    }

    .mBlock__label{
        display: block;
        font-size: 12px;
        color: #78909c;
        font-weight: 700;
        text-align: left;
    }
    .mBlock__label_radio{
        font-size: 14px;
        color: #263238;
        font-weight: 400;
        text-align: left;
    }
    .mBlock__input{
        padding: 5px 10px;
        display: block;
        font-size: 14px;
        width: calc(100% - 40px);
        height: 25px;
        margin-top: 7px;
        margin-bottom: 10px;
        border-radius: 4px;
        border: 1px solid #566270;
    }
</style>