<template>

<div class="espLogin">
    <transition :name="tpefect">
        <div v-if="show">
    <label>
        Usuario
    </label>
    <input type="text" class="form-control" v-model="userw" />
    
    <label> Contraseña  </label>
        <input type="password" class="form-control" v-model="passw" />
 <br />
 <div v-show="success" class="alert alert-success">{{msjSuccess}}</div>
 <div v-show="error" class="alert alert-danger">{{msjError}}</div>
    <div class="btn btn-info" @click="inilogin()">Ingresar</div>
    </div>
    </transition>
</div>

</template>

<style scoped>

.espLogin{
    width:100%;
    max-width:350px;
    margin:0 auto;
    padding:3%;
    border:solid 1px #ccc;
    border-radius:5px
}

input{
    box-shadow:0 0 5px #ccc;
    text-align: center;
}

input:focus{
    background-color:#000;
    color:#fff;
}
/* tipos de efectos */
/*-----fade----*/
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}

/*---slide-fade----*/
/* Las animaciones de entrada y salida pueden utilizar */
/* diferentes funciones y duraciones                   */
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active for <2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}



/*-----bounce----*/
.bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-out .5s;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes bounce-out {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(0);
  }
}

</style>
<script>
module.exports={
    data(){
        return {
            userw:"",
            passw:"",
            show:true,
            success:false,
            error:false
        }
    },
    methods:{
            inilogin(){
                var payload={
                    as:this.dirpost, ///// es un gancho que puede utilizar del lado del servidor en caso de usar un switch o un if 
                    user:this.userw, 
                    pass:this.passw
                }
                var sendata={}
            this.encrypt===true ? sendata=btoa(payload) : sendata=payload
                fetch(this.baseconect,{
                    method:'POST',
                    headers:{
                        'Content-type':'application/json'
                    },
                    body:JSON.stringify(sendata)
                })
                .then(res=>res.json())
                .then((data)=>{
                    if(data.res===1){

                        /*---emite el resultado del login segun la respuesta del servidor---*/
                        setTimeout(()=>{
                            this.$emit('reslogin',true) 
                        },1500)
                                this.success=true
                            }else{ 
                            
                             this.error=true
                    }
                    setTimeout(()=>{
                        this.error=false
                    },2000)
                    
                })
            }

    
    },
    props:{
        baseconect:{
            default:"./query.php"  /*---indica donde envia los datos para validar---*/
        },
        encrypt:{
            default:false /*---indica si los datos van encriptados y debe desencriptar del lado del servidor con base64 o sin encriptar ---*/
        },
        dirpost:{
            default:'loginarea' /*---indica del lado del servidor un parametro extra configurable en caso de utilizar switch o un if---*/
        },
        efecto:{
            default:true   /*-------activa o desactiva los efectos de animación  ----*/
        },
        tpefect:{
            default:"bounce" /*---fade,slide-fade, bounce----*/
        },
        seg:{
            default:1000  /*-------indica los segundos en que se ejecuta la animación ----*/
        },
        msjSuccess:{
            default:"Acceso correcto" /*-----indica el mensaje despues de un logeo correcto---------*/
        },
        msjError:{
            default:"Verifique sus datos son incorrectos" /*-----indica el mensaje despues de un logeo incorrecto---------*/
        }

    },
    created(){
          if(this.efecto===true){
           this.show=false
          
      }
    },
    mounted(){ 
      if(this.efecto===true){ /*-------si efecto es true se activa el efecto de aparicion de inputs ----*/

            setTimeout(()=>{
                this.show=true
            },this.seg)
      }
        
    }
}
</script>