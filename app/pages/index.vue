<template>
    <section>
        <div class="container">
            <div class="d-flex">
                <Aside />


                <div class="w-100">

                    <div class="indicator d-flex align-items-center justify-content-between">
                        <h3 class="indicator__title">
                            Заполните форму
                        </h3>
                        <div class="indicator__wrapper text-center col d-flex align-items-center justify-content-between">
                            <div class="indicator__item active col-2 px-0">1</div>
                            <div class="indicator__item active col-2 px-0">2</div>
                            <div class="indicator__item active col-2 px-0">3</div>
                            <div class="indicator__item col-2 px-0">4</div>
                            <div class="indicator__item col-2 px-0">5</div>
                        </div>
                    </div>

                    <form action="" class="my-5">
                        <h5>Общая информаия ------</h5>

                        <div class="row align-items-center">

                            <label for="" class="d-flex flex-column col-4">
                                <span>Фамилия</span>
                                <input v-model="form.surname" type="text">
                            </label>
                            <label for="" class="d-flex flex-column col-4">
                                <span>Имя</span>
                                <input v-model="form.name" type="text">
                            </label>
                            <label for="" class="d-flex flex-column col-4">
                                <span>Отчество</span>
                                <input v-model="form.patronymic" type="text">
                            </label>

                            <label for="" class="d-flex flex-column col-4">
                                <span>Меняли фамилию?</span>

                                <input type="radio" id="changeNameTwo" value="1" v-model="form.changeName">
                                <label for="changeNameTwo">Да</label>

                                <input type="radio" id="changeNameOne" value="0" v-model="form.changeName">
                                <label for="changeNameOne">Нет</label>
                            </label>
                            <label for="" class="d-flex flex-column col-4">
                                <span>Пол</span>

                                <input type="radio" id="genderOne" value="0" v-model="form.gender">
                                <label for="genderOne">Ж</label>

                                <input type="radio" id="genderTwo" value="1" v-model="form.gender">
                                <label for="genderTwo">М</label>
                            </label>

                            <label for="" class="d-flex flex-column col-4">
                                <span>Семейное положение</span>
                                <select
                                        v-model="form.maritalStatus"
                                        v-if="arrayMaritalStatus.length" name="" id="">
                                    <option
                                            v-for="item in arrayMaritalStatus"
                                            :key="item.id"
                                            :value="item.id">
                                        {{ item.name }}
                                    </option>
                                </select>
                            </label>
                            <label for="" class="d-flex flex-column col-4">
                                <span>Гражданство</span>
                                <select
                                        v-model="form.citizenship"
                                        v-if="arrayCitizenship.length" name="" id="">
                                    <option
                                            v-for="item in arrayMaritalStatus"
                                            :key="item.id"
                                            :value="item.id">
                                        {{ item.name }}
                                    </option>
                                </select>
                            </label>

                            <label for="" class="d-flex flex-column col-4">
                                <span>Дата рождения</span>
                                <input v-model="form.dateBirth" type="date">
                            </label>

                            <label for="" class="d-flex flex-column col-12">
                                <span>Место рождения</span>
                                <input v-model="form.placeBirth" type="text">
                                <span>
                                    Например, Россия, Комсомольск-на-Амуре
                                </span>
                            </label>


                        </div>

                    </form>
                    <div>
                        <button @click="prev" class="btn btn-info">Назад</button>
                        <button @click="next" class="btn btn-success">Дальше</button>
                    </div>

                </div>


            </div>
        </div>
    </section>
</template>

<script>
    import Aside from "../components/Aside";
export default {
    components:{
        Aside
    },
    data: () => ({
        form:{
            surname: '',
            name: '',
            patronymic: '',
            changeName: '0',
            gender: '1',
            maritalStatus: null,
            citizenship: null,
            dateBirth: '',
            placeBirth: ''
        },
        arrayMaritalStatus: [
            { id: 1, name: 'potap' }
        ],
        arrayCitizenship: [
            { id: 1, name: 'potap' }
        ],
    }),
    mounted(){
        this.form.maritalStatus = this.arrayMaritalStatus[0].id;
        this.form.citizenship = this.arrayCitizenship[0].id;

        if (localStorage.getItem('saveForm') !== null)
        {
            this.form =  JSON.parse(localStorage.getItem('saveForm'));
        }
    },
    methods:{
        next()
        {
            localStorage.setItem('saveForm', JSON.stringify(this.form));
        },
        prev()
        {
            delete localStorage.saveForm;
        }
    }
}
</script>
