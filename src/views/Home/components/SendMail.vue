<template>
    <section class="email">
      <div class="container">
           <Title :sub="subtitlevido" :title="title" />
           <div class="form">
               <ul>
                   <li><a href=""><i class="fas fa-sign-in"></i>используется кнопка</a></li>
                   <li><a href=""><i class="fas fa-sign-in"></i>используется</a></li>
                   <li><a href=""><i class="fas fa-sign-in"></i>нопка Submit</a></li>
               </ul>
               <form @submit.prevent="sendMail">
                   <input type="text" :class="{ border: borderof1  }" placeholder="Your name..." v-model="Name">
                   <input type="tel" :class="{ border: borderof2  }" placeholder="+998(88)183-68-68" v-model="tel">
                   <textarea placeholder="Comment..." :class="{ border: borderof3  }" v-model="Comment"></textarea>
                   <Button type="submit">Sends</Button>
               </form>
           </div>
      </div>
    </section>
</template>


<script>
import Title from '@/layouts/Title.vue'
import Button from '@/layouts/Button.vue'

export default {
  components: {
    Title,
    Button,
  },
  data(){
    return{
      borderof1: false,
      borderof2: false,
      borderof3: false,  
      subtitlevido: 'Formni to`g`ri to`ldiring va men siz bilan albatta bog`lanaman ok?',
      title: 'Akhmadov G`anisher contacts',
      Name: '',
      tel: '',
      Comment: '',
      Tokin: '5247852882:AAH-v3nzD-kFRm1P9M4D2P-iGuMBOrcGfBg',
      Chatid: '-649993032',
    
    }
  },
  methods: {
    async sendMail(){
      

        if(this.Name.length > 0 && this.tel.length > 0 && this.Comment){

           const ism = String('Ismi:'+this.Name);
           const tel = String('Tel Raqami:'+this.tel);
           const com = String('Izoxi:'+this.Comment);

           await fetch(`https://api.telegram.org/bot${this.Tokin}/sendMessage?chat_id=${this.Chatid}&parse_mode=html&text=${ism},${tel},${com}`);
           this.Name = '';
           this.tel = '';
           this.Comment = '';
        }

    
        

    }
  }     
   
}
</script>


<style lang="scss">
@import '../../../assets/styles/components/_vars.scss';
@import '../../../assets/styles/components/_mixins.scss';
 
 
    .email{
        background: url('../../../assets/images/layout/sec-bg.jpg') no-repeat center / cover;
        color: $white;
        padding: 100px 0;

        .form{
           display: flex;
           justify-content: space-around;
           align-items: center;
           flex-wrap: wrap;
           padding: 70px 0 0 0;
           form{
               background: $white;
               padding: 20px;
               width: 350px;
               height: 400px;
               display: flex;
               flex-direction: column;
               justify-content: space-between;
               align-items: center;
               border-radius: 4px;
               //Media
               @include md{
                   margin-top: 30px;
               }
               textarea{
                   width: 100%;
                   height: 100px;
                   padding: 15px;
                   font-size: 18px;
                   border: 1px solid $border_color;
               }
               input{
                   width: 100%;
                   height: 50px;
                   padding: 0 15px;
                   font-size: 18px;
                   border: 1px solid $border_color;
               }
               .border{
                   border: 2px solid red;
               }
           }
           ul{
               li{
                   list-style: none;
                   padding: 12px 0;

                   a{
                       color: $bg_color;
                       font-size: 18px;
                       display: flex;
                       justify-content: flex-start;
                       align-items: center;
                       i{
                           margin-right: 14px;
                       }

                   }
               }
           }
        }

    }
</style>