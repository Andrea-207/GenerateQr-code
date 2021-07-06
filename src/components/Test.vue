<template>

<div class="container">
    <div class="row">
        <div class=" d-flex justify-content-center rocket">
            <img class="img-size" src="../assets/icons8-razzo-unscreen.gif"/>
        </div>
        <div class="col-md-12">
                <h1 class="text-decoration">QR Code Generate</h1>
            <div>
                <input class="input" type="text" placeholder="insert your link" v-model="link" >
                <button class="button" @click="change()">send</button>
            </div>
            <div class="output">
                <vue-qrcode class="img-color" :value="TextValue" />   
            </div>
        </div>
    </div>
        <div>
            <button class="" @click="onClick()">Download File</button>
        </div>
        <footer class="footer">
            <p class="">© 2021 <a href="https://promptsolutions.it/">Prompt Solutions S.r.l.s.</a> – Tutti i diritti riservati – Policy Privacy</p>
        </footer>       
</div>

</template>


<script>
import VueQrcode from 'vue-qrcode';
import axios from 'axios';

export default {
    components: {
        VueQrcode,
    }, 
    data(){
        return{
            TextValue:'',
            link: ''
        }
    },
    methods:{
        change() {
            this.TextValue = this.link;
        },          
        onClick(){
            axios({
                url:"http://www.teologiafermo.it/img/public/Docenti/Andreozzi_Prof._don_Andrea.jpg",
                methods:'GET',
                responseType:'blob'
            }).then((response) => {
                var fileUrl = window.URL.createObjectURL(new Blob([response.data]))
                var fileLink = document.createElement('a')
                fileLink.href = fileUrl

                fileLink.setAttribute('download', 'image.jpg')
                document.body.appendChild(fileLink)
                fileLink.click()
                console.log(this.onClick)
            })
        }   
    },
}

</script>

<style>
body{
    min-height: 100vh;
    background-color: #00ff5571 ;
}


.output{
    margin-top: 35px;
}
.output img{
    box-shadow: 0px 5px 11px 12px rgba(168,140,220,0.75);
    -webkit-box-shadow: 0px 5px 11px 12px rgba(168,140,220,0.75);
    -moz-box-shadow: 0px 5px 11px 12px rgba(168,140,220,0.75);
}


.button{
    background-image: linear-gradient(12deg, #3fcfe228 0%, #7a64f2 100%);
    border-radius: 8px ;
    margin-left: 25px;
    color: rgba(255, 255, 255, 0.856);
    font-weight: bold;
    width: 6%;
    padding: 2px;
    border: 1px solid whitesmoke;
}
.input{
    border-radius: 6px;
    border: 1px solid #5a49f8;
    padding: 2px;
}
input:focus{
    outline: none;
}

.text-decoration{
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    font-size: 45px;
}
.text-decoration:hover{
    color: whitesmoke;
}
.img-size{
    width: 65px;
    height: 65px;
    color: #00ff5571;

}
.rocket{
    width: 100px;
    margin-right: 150px;
    margin: 0 !important;
    position: relative;
    animation-name: example;
    animation-duration: 15s;
    animation-delay: 2s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
    display: flex;
    
}
@keyframes example {
  0%   { left:0px; top:0px;}
  25%  { left:91.2%; top:0px;}
  50%  { left:91.2%; top:450px;}
  75%  { left:0px; top:450px;}
  100% { left:0px; top:0px;}
}
.footer{
    display: flex;
    justify-content: center;
    margin-top: 35%;
}


</style>