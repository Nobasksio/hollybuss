<template >
    <div class="container" >

        <div class="row" >
            <div class="col-12" >
                <div class="first" v-show="show['show1']" >
                    <h1 class="text-center pt-3" >Привет, друг! </h1 >
                    <img src="/img/tela.png" class='img-fluid px-5 py-3' alt="" >

                    <div class="card" >
                        <div class="card-body my-card" >
                            Общественный транспорт должен и может быть не менее удобным чем такси.
                            <p >Садись прокачу!</p >
                            <!--Мы хотим сделать общественный транспорт крутым,-->
                            <!--удобным и чистым. Расскажи нам о последней поездке и-->
                            <!--получи приятный бонус.-->
                            <div >
                                <b-button pill block
                                          variant="primary"
                                          class="button-gradient my-booton py-3 mt-3 mb-2" @click="next(2)" >Погнали!
                                </b-button >
                            </div >
                        </div >
                    </div >
                </div >
                <div class="sixth" v-show="show['show2']" >
                    <div class="row" >
                        <div class="h100" >

                            <map2></map2>
                            <!--<div id="map2" v-show="state_map" :class="{map2:state_map, map:!state_map}" >-->
                            <!--</div >-->

                            <div class="fixed" v-show="!state_map" >
                                Иркутск, Игошина 1а
                                <br >
                                <span class="sudtext" >
                                ваш адрес
                            </span >
                            </div >
                            <div class="fixed-input px-3" v-show="!state_map" >
                                <!--<b-form-input v-model="form.mut" class='where' placeholder="Куда едем" ></b-form-input >-->
                                <multiselect v-model="form.to"
                                             :options="adresses"
                                             :placeholder="placeholder"
                                             label="name"
                                             track-by="name"
                                ></multiselect >
                                <b-button pill block variant="primary" class="my-booton py-3 mt-3 mb-4 "
                                          @click="route(1)" >Мчим!
                                </b-button >
                            </div >
                        </div >
                    </div >
                </div >
                <div class="sixth" v-show="show['show3']" >
                    <div class="row" >
                        <div class="h100" >
                            <div id="map2" class="map2 c-map__embeds" >
                            </div >
                            <!--<map2></map2>-->
                            <div class="map2_card" >
                                <b-input-group size="lg" class="pt-3 px-3" >
                                    <b-input-group-text class='' slot="prepend"><strong class="input-size">A</strong></b-input-group-text>
                                    <b-form-input v-model="form.from" class="input-size"></b-form-input >
                                </b-input-group >
                                <b-input-group size="lg" class="pt-3 px-3 input-size" >
                                    <b-input-group-text class='input-size' slot="prepend"><strong class="input-size">B</strong></b-input-group-text>
                                    <b-form-input v-model="form.to.name" class="input-size"></b-form-input >
                                </b-input-group >

                                <div class="container pb-4" v-show="route_num == null">
                                    <h4 class="pt-3 pt-2">Найдено <span class="blue">4</span> маршрута:</h4 >
                                    <b-button variant="outline-secondary"
                                              class="route-card border-0 px-4"
                                              @click="route_set('16')"
                                              :class="{selected_butt:route_num == '16' }">16</b-button>
                                    <b-button variant="outline-secondary"
                                              class="route-card border-0 px-4"
                                              @click="route_set('16k')"
                                              :class="{selected_butt:route_num == '16k' }">16k</b-button>
                                    <b-button variant="outline-secondary"
                                              class="route-card border-0 px-4"
                                              @click="route_set('17l')"
                                              :class="{selected_butt:route_num == '17l' }">17l</b-button>
                                    <b-button variant="outline-secondary"
                                              class="route-card border-0 px-4"
                                              @click="route_set('90s')"
                                              :class="{selected_butt:route_num == '90s' }">90s</b-button>
                                </div>
                                <div class="container pt-2" v-show="route_num != null">
                                    Водитель Ибрагим ожидает Вас на газели номер: <span class="blue"> {{ route_num }}</span>
                                    <br>
                                    через:<span class="blue"> 15 минут</span> <br>
                                    на остановке: <span class="blue">ИРГТУ  </span>
                                    <p class="pt-2 bold">
                                        Выходите прямо сейчас чтобы успеть.
                                    </p>
                                    <div class="row justify-content-between mb-4">
                                        <b-button variant="outline-danger"
                                                  class="route-card border-0 px-4 mx-4"
                                                  @click="route_set('90s')"
                                        >Транспорта нет</b-button>
                                        <b-button variant="outline-secondary"
                                                  class="route-card border-0 px-4 mx-4 selected_butt"
                                                  @click="next(4)"
                                        >Я сел</b-button>
                                    </div>
                                </div>
                            </div >


                        </div >
                    </div >
                </div >
                <div class="first" v-show="show['show4']" >
                    <h1 class="text-center pt-3" >Как поездочка? </h1 >
                    <img src="/img/01_Montazhnaya_oblast_1_kopia.png" class='img-fluid px-5 py-3' alt="" >

                    <div class="card" >
                        <div class="card-body my-card" >
                            Мы хотим сделать общественный транспорт крутым,
                            удобным и чистым.
                            <p class="pt-2">Расскажи нам о последней поездке на маршруте <span class="blue"> номер {{ route_num }}</span>, сделай мир лучше и
                                получи приятный бонус.</p>
                            <p class="bold">Улучшай!</p >

                            <div >
                                <b-button pill block
                                          variant="primary"
                                          class="button-gradient my-booton py-3 mt-3 mb-2" @click="next(5)" >Вжух!
                                </b-button >
                            </div >
                        </div >
                    </div >
                </div >
                <!--<div class="second" v-show="show['show4']" >-->
                    <!--<div class="row pt-3" >-->
                        <!--<div class="col-2" @click="back(1)" ><img src="/img/left-arrow.svg" alt="" class="img-fluid" >-->
                        <!--</div >-->
                        <!--<div class="col-8" ><h1 class="text-center" >Шаг 1 из 3</h1 ></div >-->
                        <!--<div class="col-1" ></div >-->
                    <!--</div >-->
                    <!--<img src="/img/bus2.png" class='img-fluid px-5 pt-3 pb-3' alt="" >-->
                    <!--<h3 class="text-center py-3" >Введи номер маршрута </h3 >-->
                    <!--<div class="card" >-->
                        <!--<div class="card-body my-card" >-->
                            <!--<multiselect v-model="form.number"-->
                                         <!--:options="options"-->
                                         <!--:custom-label="nameWithLang"-->
                                         <!--placeholder="например 16к"-->
                                         <!--label="name"-->
                                         <!--track-by="name"-->
                            <!--&gt;</multiselect >-->
                            <!--<div >-->
                                <!--<b-button pill block-->
                                          <!--variant="primary"-->
                                          <!--class="my-booton py-3 mt-3 mb-2" @click="next(3)" >Далее-->
                                <!--</b-button >-->
                            <!--</div >-->
                        <!--</div >-->
                    <!--</div >-->
                <!--</div >-->
                <div class="third" v-show="show['show5']" >

                    <div class="row pt-3" >
                        <div class="col-2" @click="back(2)" ><img src="/img/left-arrow.svg" alt="" class=" img-fluid" >
                        </div >
                        <div class="col-8" ><h1 class="text-center" >Шаг 1 из 2</h1 ></div >
                        <div class="col-1" ></div >
                    </div >
                    <img src="/img/man.png" class='img-fluid px-5 pt-3 pb-3' alt="" >
                    <h3 class="text-center py-3" >Оставь свою оценку </h3 >
                    <div class="card my-card " >
                        <div class="card-body mx-auto" >
                            <b-button-group >
                                <b-button variant="outline-secondary " class='butgroup'
                                          :class="{button_for_group : form.rait==1}" @click="form.rait = 1" >1
                                </b-button >
                                <b-button variant="outline-secondary " class='butgroup'
                                          :class="{button_for_group : form.rait==2}" @click="form.rait = 2" >2
                                </b-button >
                                <b-button variant="outline-secondary " class='butgroup'
                                          :class="{button_for_group : form.rait==3}" @click="form.rait = 3" >3
                                </b-button >
                                <b-button variant="outline-secondary " class='butgroup'
                                          :class="{button_for_group : form.rait==4}" @click="form.rait = 4" >4
                                </b-button >
                                <b-button variant="outline-secondary " class='butgroup'
                                          :class="{button_for_group : form.rait==5}" @click="form.rait = 5" >5
                                </b-button >
                            </b-button-group >
                        </div >
                        <div class="mx-4 " >
                            <b-button pill block variant="primary" class="my-booton py-3 mt-3 mb-4 " @click="next(6)" >
                                Далее
                            </b-button >
                        </div >
                    </div >

                </div >
                <div class="forth" v-show="show['show6']" >
                    <div class="row pt-3" >
                        <div class="col-2" @click="back(3)" ><img src="/img/left-arrow.svg" alt="" class=" img-fluid" >
                        </div >
                        <div class="col-8" ><h1 class="text-center" >Шаг 2 из 2</h1 ></div >
                        <div class="col-1" ></div >
                    </div >
                    <div class="card my-card mt-3" >
                        <div class="card-body mx-auto" >

                            <h4 class="pb-2" >
                                Что вам не понравилось?
                            </h4 >

                            <div class="row" >
                                <div class="col text-center" @click="toogle('transport')" >
                                    <div class="card my-card2 p-2 " :class="{'border-my' : form.transport}" >
                                        <img src="/img/01-05.png" alt="" class="img-fluid" >
                                    </div >
                                    <span class="font-12" >Транспорт</span >
                                </div >
                                <div class="col text-center px-1" @click="toogle('driver')" >
                                    <div class="card my-card2 p-2" :class="{'border-my' : form.driver}" >
                                        <img src="/img/01-07.png" alt="" class="img-fluid" >
                                    </div >
                                    <span class="font-12" >Водитель</span >
                                </div >
                                <div class="col text-center" @click="toogle('route')" >
                                    <div class="card my-card2 p-2" :class="{'border-my' : form.route}" >
                                        <img src="/img/01-06.png" alt="" class="img-fluid" >
                                    </div >
                                    <span class="font-12" >Маршрут</span >
                                </div >

                            </div >

                            <div class="pt-3" >
                                <h4 class="pb-2" >
                                    Что было не так?
                                </h4 >
                                <multiselect v-model="form.number"
                                             :options="options_problem"
                                             placeholder="например 16к"
                                             label="name"
                                             track-by="name"
                                ></multiselect >
                                <h4 class="pt-4 pb-2" >
                                    Опишите подробнее
                                </h4 >
                                <b-form-textarea
                                        id="textarea"
                                        v-model="form.comment"
                                        placeholder="Enter something..."
                                        rows="3"
                                        max-rows="6"
                                ></b-form-textarea >
                            </div >


                        </div >
                        <div class="mx-4 " >
                            <b-button pill block variant="primary" class="my-booton py-3 mt-3 mb-4 " @click="next(7)" >
                                Отправить
                            </b-button >
                        </div >
                    </div >

                </div >
                <div class="fifth" v-show="show['show7']" >
                    <h1 class="text-center pt-5" >Спасибо за твой <br >первый отзыв!</h1 >

                    <img src="/img/thanks.png" class='img-fluid px-5 py-3' alt="" >
                    <div class="text-center py-4" >
                        Ты получаешь <span class="bold" >скидку 10 % </span >
                        <br >
                        в Sushi-Studio
                    </div >
                    <div class="mx-4 " >
                        <b-button pill block variant="primary" class="my-booton py-3 mt-3 mb-4 " >Спасибо за внимание
                        </b-button >
                    </div >
                </div >

            </div >
        </div >
    </div >
</template >

<script >

    export default {
        name: "welcome",
        data: function () {
            return {

                coords: [52, 104],
                show: {
                    'show1': true,
                    'show2': false,
                    'show3': false,
                    'show4': false,
                    'show5': false,
                    'show6': false,
                    'show7': false,
                },
                adresses:[
                     {name: 'г. Иркутск, Гоголя 15', language: ''},
                    {name: 'г. Иркутск, Академическая 22', language: ''},
                ],
                placeholder:'Куда едем?',
                state_map: false,
                markerIcon: {
                    layout: 'default#imageWithContent',
                    imageHref: 'https://image.flaticon.com/icons/png/512/33/33447.png',
                    imageSize: [43, 43],
                    imageOffset: [0, 0],
                    content: '123 v12',
                    contentOffset: [0, 15],
                    contentLayout: '<div style="background: red; width: 50px; color: #FFFFFF; font-weight: bold;">$[properties.iconContent]</div>'
                },
                route_num:null,
                validate: {
                    'val1': true,
                    'val2': false,
                    'val3': false,
                    'val4': false,
                    'val5': false,
                },
                form: {
                    number: null,
                    rait: null,
                    'transport': false,
                    'driver': false,
                    'route': false,
                    comment: null,
                    from: 'г. Иркутск, ул Игошина 1а',
                    to:'г. Иркутск, Гоголя 15',
                },
                options: [
                    {name: '16к', language: 'маршрутка'},
                    {name: '80', language: 'автобус'},
                    {name: '90', language: 'автобус'},
                    {name: '10', language: 'трамвай'},
                    {name: '3', language: 'троллейбус'}
                ],
                options_problem: [
                    {name: 'Машина каптила', language: 'маршрутка'},
                    {name: 'Спущенное колесо', language: 'автобус'},
                    {name: 'Все дребезжало', language: 'автобус'},
                    {name: 'Пахло бензином', language: 'трамвай'},
                    {name: 'Водитель курил', language: 'троллейбус'}
                ],
            }
        },
        methods: {
            route_set: function(seted_route){
                this.route_num = seted_route;
                this.show['show8'] = true;
            },
            route: function (route) {
                this.show['show2'] = false;
                this.show['show3'] = true;
                this.state_map = true;


                var myMap2 = new ymaps.Map("map2", {
                    // Координаты центра карты.
                    // Порядок по умолчанию: «широта, долгота».
                    // Чтобы не определять координаты центра карты вручную,
                    // воспользуйтесь инструментом Определение координат.
                    center: [52.261543, 104.265431],
                    // Уровень масштабирования. Допустимые значения:
                    // от 0 (весь мир) до 19.
                    zoom: 12,
                    controls: []

                });
                var multiRoute2 = new ymaps.multiRouter.MultiRoute({
                    // Точки маршрута. Точки могут быть заданы как координатами, так и адресом.
                    referencePoints: [
                        'Иркутск, Игошина 1а',
                        'Иркутск, Академическая 10', // улица Льва Толстого.
                    ], params: {
                        // Тип маршрута: на общественном транспорте.
                        routingMode: "masstransit"
                    }
                }, {

                    boundsAutoApply: true
                });

                myMap2.geoObjects.add(multiRoute2);

                if (route == 1) {
                    $('#map').html('');

                    var myMap = new ymaps.Map("map", {
                        // Координаты центра карты.
                        // Порядок по умолчанию: «широта, долгота».
                        // Чтобы не определять координаты центра карты вручную,
                        // воспользуйтесь инструментом Определение координат.
                        center: [52.261543, 104.265431],
                        // Уровень масштабирования. Допустимые значения:
                        // от 0 (весь мир) до 19.
                        zoom: 12,
                        controls: []

                    });
                    var multiRoute = new ymaps.multiRouter.MultiRoute({
                        // Точки маршрута. Точки могут быть заданы как координатами, так и адресом.
                        referencePoints: [
                            'Иркутск, Игошина 1а',
                            'Иркутск, Гоголя 15', // улица Льва Толстого.
                        ], params: {
                            // Тип маршрута: на общественном транспорте.
                            routingMode: "masstransit"
                        }
                    }, {
                        boundsAutoApply: true
                    });
                    myMap.geoObjects.removeAll();
                    myMap.geoObjects.add(multiRoute);
                } else {
                    window.add1();
                }
            },
            nameWithLang({name, language}) {
                return `${name} — ${language}`
            },
            next: function (next_number) {


                let name_var = 'show' + next_number;
                let pre_name_var = 'show' + (next_number - 1);
                this.show[pre_name_var] = false;

                this.show[name_var] = true;

            },
            back: function (back_number) {
                let name_var = 'show' + back_number;
                let pre_name_var = 'show' + (back_number + 1);

                this.show[pre_name_var] = false;

                this.show[name_var] = true;
            },
            toogle: function (toogle_el) {
                console.log(toogle_el)
                if (this.form[toogle_el] == false) {
                    this.form[toogle_el] = true
                } else {
                    this.form[toogle_el] = false

                }
            }
        }
    }
</script >

<style scoped >
    body {
        background: #FFFFFF;
        color: #33516F;

    }

    h1 {
        color: #33516F;
        font-size: 24px;
        font-family: ab;
    }

    h3 {
        color: #3D3C3C;
        font-size: 22px;
        font-family: ab;
    }

    h4 {
        Font-Size: 16px;
        font-family: ab;
    }

    .my-card {
        background: #FFFFFF;
        box-shadow: 0px 4px 35px rgba(0, 0, 0, 0.08);
        border-radius: 22px;
    }

    .my-card2 {
        border-radius: 8px
    }

    .my-booton {
        background: linear-gradient(180deg, #130FCC 0%, #350DA9 100%);
        font-family: ab;
    }

    .button_for_group {
        background: linear-gradient(180deg, #130FCC 0%, #350DA9 100%);
        color: #ffffff;
    }

    .butgroup {
        padding: 10px 20px;
    }

    .font-12 {
        font-size: 12px;
    }

    .border-my {
        border-color: #140FCB;
    }

    .bold {
        font-family: ab;
    }


    .map {
        width: 100%;
        height: 100vh;
    }

    .map2 {
        width: 100%;
        height: 70vh;
        z-index: 3324234223;
        position: relative;
    }

    .map2_card {
        width: 100%;
        height: 30vh;
        border-radius: 22px 0 0 22px;

    }

    .h100 {
        height: 100vh;
        width: 100%;
    }

    .fixed {
        width: 100%;
        font-size: 30px;
        text-align: center;
        position: absolute;
        top: 100px;
        font-family: am;
    }

    .fixed-input {
        width: 100%;
        position: absolute;
        bottom: 100px;
    }

    .where {
        width: 100%;
        box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.25);
        border-radius: 8px;
        height: 40px;
    }

    .sudtext {
        font-family: ar;
    }
    .blue{
        color: #140FCB;
    }
    .selected_butt{
        background: #140FCB;
        color:#FFFFFF;
    }
    .route-card{
        border-radius: 22px;
        box-shadow: 0px 4px 35px rgba(0, 0, 0, 0.1);
    }
    .input-size{
        font-size: 14px;
    }
</style >