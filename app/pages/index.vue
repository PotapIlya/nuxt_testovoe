<template>
    <section>
        <div class="container">
            <div class="d-flex">
                <Aside />


                <div class="w-100">

                    <div
                            class="indicator flex-column flex-md-row d-flex align-items-center justify-content-between">
                        <h3 class="indicator__title mb-2 mb-md-0">
                            Заполните форму
                        </h3>
                        <div v-if="arrayIndicator.length"
                                class="indicator__wrapper text-center col d-flex align-items-center justify-content-between">

                            <div
                                    v-for="(item, index) in arrayIndicator"
                                    class="indicator__item col px-0"
                                    :class="{ active : item.status }"
                                    @click="changeIndicator(index)"
                            >
                                {{ item.label}}
                            </div>
                        </div>
                    </div>

                    <div class="form__wrapper my-3">
                        <h6 class="form__title">Общая информация</h6>

                        <div class="row align-items-center">

                            <label for="" class="d-flex flex-column col-6 col-md-4">
                                <span>Фамилия</span>
                                <input v-model="dataForm.surname" type="text">
                            </label>
                            <label for="" class="d-flex flex-column col-6 col-md-4">
                                <span>Имя</span>
                                <input v-model="dataForm.name" type="text">
                            </label>
                            <label for="" class="d-flex flex-column col-6 col-md-4">
                                <span>Отчество</span>
                                <input v-model="dataForm.patronymic" type="text">
                            </label>

                            <label for="" class="changeName d-flex flex-column col-6 col-md-4">
                                <span>Меняли фамилию?</span>

                                <div class="d-flex align-content-center">
                                    <input type="radio" class="d-none" id="changeNameTwo" value="1" v-model="dataForm.changeName">
                                    <label
                                            :class="{ 'active' : dataForm.changeName === '1' }"
                                            for="changeNameTwo"
                                    >
                                        Да
                                    </label>

                                    <input class="d-none" type="radio" id="changeNameOne" value="0" v-model="dataForm.changeName">
                                    <label
                                            :class="{ 'active' : dataForm.changeName === '0' }"
                                            for="changeNameOne"
                                    >
                                        Нет
                                    </label>
                                </div>

                            </label>
                            <label for="" class="changeName d-flex flex-column col-6 col-md-4">
                                <span>Пол</span>

                                <div class="d-flex align-items-center">
                                    <input class="d-none" type="radio" id="genderOne" value="0" v-model="dataForm.gender">
                                    <label :class="{ 'active' : dataForm.gender === '0' }" for="genderOne">Ж</label>

                                    <input class="d-none" type="radio" id="genderTwo" value="1" v-model="dataForm.gender">
                                    <label :class="{ 'active' : dataForm.gender === '1' }" for="genderTwo">М</label>
                                </div>
                            </label>

                            <label for="" class="d-flex flex-column col-6 col-md-4">
                                <span>Семейное положение</span>
                                <select
                                        v-model="dataForm.maritalStatus"
                                        v-if="arrayMaritalStatus.length" name="" id="">
                                    <option
                                            v-for="item in arrayMaritalStatus"
                                            :key="item.id"
                                            :value="item.id">
                                        {{ item.name }}
                                    </option>
                                </select>
                            </label>
                            <label for="" class="d-flex flex-column col-6 col-md-4">
                                <span>Гражданство</span>
                                <select
                                        v-model="dataForm.citizenship"
                                        v-if="arrayCitizenship.length" name="" id="">
                                    <option
                                            v-for="item in arrayMaritalStatus"
                                            :key="item.id"
                                            :value="item.id">
                                        {{ item.name }}
                                    </option>
                                </select>
                            </label>

                            <label for="" class="d-flex flex-column col-6 col-md-4">
                                <span>Дата рождения</span>
                                <input v-model="dataForm.dateBirth" type="date">
                            </label>

                            <label for="" class="d-flex flex-column col-12">
                                <span>Место рождения</span>
                                <input v-model="dataForm.placeBirth" type="text">
                                <span class="dataForm__greyText">
                                    Например, Россия, Комсомольск-на-Амуре
                                </span>
                            </label>


                        </div>

                    </div>
                    <div class="buttonsPage d-flex justify-content-between align-items-center">
                        <button @click="prev" class="btn btn-info">Назад</button>
                        <button @click="next" class="btn btn-success">Дальше</button>
                    </div>

                </div>


            </div>
        </div>
    </section>
</template>

<script>
    import Aside from "../components/basic/Aside";
export default {
    components:{
        Aside
    },
    data: () => ({
        dataForm:{
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

        arrayIndicator: [
            { label: 1, status: true },
            { label: 2, status: false },
            { label: 3, status: false },
            { label: 4, status: false },
            { label: 5, status: false },
        ]
    }),
    mounted(){
        this.dataForm.maritalStatus = this.arrayMaritalStatus[0].id;
        this.dataForm.citizenship = this.arrayCitizenship[0].id;

        if ( localStorage.getItem('saveForm') )
        {
            this.dataForm = JSON.parse(localStorage.getItem('saveForm'));
        }
    },
    methods:{
        next()
        {
            localStorage.setItem('saveForm', JSON.stringify(this.dataForm));
        },
        prev()
        {
            this.dataForm = {
                surname: '',
                name: '',
                patronymic: '',
                changeName: '0',
                gender: '1',
                maritalStatus: null,
                citizenship: null,
                dateBirth: '',
                placeBirth: ''
            };
            localStorage.removeItem('saveForm');
        },
        changeIndicator(id)
        {
            this.arrayIndicator.forEach( item => item.status = false );
            this.arrayIndicator.forEach( (item, index) => {
                if (index <= id){
                    item.status = true
                }
            })
        }
    }
}
</script>
