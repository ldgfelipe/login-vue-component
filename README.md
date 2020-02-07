Componete compatible con CDN vuejs  y Bootstrap
Se integra el componente con las propiedades que puede modificar el componente 


Atriburos modificables de login

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
            default:"fade" /*---fade,slide-fade, bounce----*/
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
        

 
 
