# Vite-Element

## Description

This template should help get you started developing with vue 3, elementUI, vue-router and axios in Vite.The template uses vue 3 <script setup> SFCs, check out the script setup docs to learn more.



## Install



```shell

npm install -g vite-element

```







## Usage



Use command to create a new project.



```shell

vite-element create MyProject

```



If the directory already exists, you can use the `-f` parameter to overwrite it.



```shell

vite-element create -f MyProject

```



## Advanced



### router



The template has helped you configure the vue-router. You just need to create a vue file and reference it in file `router/routes.js`.



```js

const routes = [

    {

        path: '/',

        name: 'home',

        meta: { title: 'home', isAuth: false },     //User need the token to acess this page, when isAuth is true

        component:()=>import('./../views/home.vue')

    },

    //Add more here...

]



```



For more information, please refer to [vue-router documents](https://router.vuejs.org/)



### axios



Axios is a *[promise-based](https://javascript.info/promise-basics)* HTTP Client for [`node.js`](https://nodejs.org/) and the browser. It is *[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application)* (= it can run in the browser and nodejs with the same codebase). On the server-side it uses the native node.js `http` module, while on the client (browser) it uses XMLHttpRequests.



Using the template, you don't need to encapsulate it again and only need to write your API in `utils/axios/api.js`.



```js

import request from './request'

export class MyService{

    //Assuming this is your API

    static async getTest(params) {

        return request.getReq('/apiSer/api/Test/testGet',params)

    }

}

```



You can use this interface as follows



```js

/* home.vue */

import {MyService} from './../utils/axios/api'

const params = {

}



MyService.getTest(params).then((res)=>{

    console.log(res.data)

}).catch((err)=>{

    console.log(err)

})

```



Please set cross domain in `vite.config.js`.



```js

import { defineConfig } from 'vite'

import vue from '@vitejs/plugin-vue'



// https://vitejs.dev/config/

export default defineConfig({

  plugins: [vue()],

  server: {

    proxy: {

      '/apiSer': {

        target: 'https://localhost:9000/',

        changeOrigin: true,

        secure: false,

        rewrite: (path) => path.replace(/^\/apiSer/, '')

      }

    }

  }

})



```







You can see [Axios documents](https://axios-http.com/docs/intro) to get more help.







### validate



The section is used for `<el-form>` rule validation. 



```vue

<!-- home.vue -->

<script setup>

import { ref,reactive } from "vue";

import validate from './../utils/validate/index'



const formRef = ref()

const data = reactive({

    form: {

        email:''

    },

    rules: {

        email: [

            { required: true, message: 'Please input email', trigger: 'blur' },

            {validator:validate.valEmail,trigger:'blur'}

        ]

    }

})



const onSubmitBtnClicked = () => {

    console.log("Check button is clicked")

}

</script>



<template>

    <el-form :model="data.form" :rules="data.rules" ref="formRef">

        <el-form-item prop="email" label="Email">

            <el-input v-model="data.form.email" />

        </el-form-item>

        <el-form-item>

            <el-button type="primary" @click="validate.checkFormFormat(formRef,onCheckBtnClicked)">Submit</el-button>

        </el-form-item>

    </el-form>

</template>



<style scoped>



</style>

```



Please refer to [Element Plus documents](https://element-plus.gitee.io/en-US/guide/design.html) for more information.







### hash



`hash.js` defined some encryption methods to encrypt some content, such as passwords.



```js

import hash from './../utils/hash/index'



console.log(hash.Md5Encryption('123456'))

```







## Github


[CairBin/ViteElementTemplate: This template should help get you started developing with vue 3, elementUI, vue-router and axios in Vite. (github.com)](https://github.com/cairbin/ViteElementTemplate)