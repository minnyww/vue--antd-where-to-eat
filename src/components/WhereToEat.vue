<template>
   <div>
      <div
         style="display:flex; justify-content : space-between; align-items : center;"
      >
         <div class="covid" style="text-align : center;">
            <div>
               <h2 style="color:#2d348c; ">
                  Covid Update
               </h2>
            </div>
            <h1>
               {{ covidData.NewConfirmed }}
            </h1>
         </div>
         <div
            :class="[
               pmData < 50
                  ? 'covid green'
                  : pmData < 100
                  ? 'covid yellow'
                  : pmData < 150
                  ? 'covid orange'
                  : pmData < 200
                  ? 'covid red'
                  : pmData < 300
                  ? 'covid purple'
                  : pmData < 500
                  ? 'covid darkpurple'
                  : 'covid',
            ]"
            style="text-align : center;"
         >
            <h2 style="color:#2d348c;">PM 2.5</h2>
            <h1>{{ pmData }}</h1>
         </div>
      </div>
      <div class="where">
         <h1>{{ msg }}</h1>
         <h1 style="margin-bottom : 0em;">ร้าน</h1>
         <h2 id="wheretoeat">{{ whereToEat.name }}</h2>
         <h1 style="margin-bottom : 0em;">รายละเอียด</h1>
         <h3 style="color : #fe5f55;">
            {{ whereToEat.description }}
         </h3>
         <a-button
            class="find-eat"
            type="primary"
            size="large"
            @click="handleRandomRestaurant"
            >กดเพื่อหาที่รับประทานข้าว</a-button
         >
      </div>
   </div>
</template>

<script>
export default {
   name: "WhereToEat",
   props: {
      msg: String,
   },
   mounted() {
      console.log("mount");
      fetch(
         "https://api.waqi.info/feed/bangkok/?token=5232bcfe545ac35f1a71737d4d1663e4e711da78",
      )
         .then((res) => res.json())
         .then(({ data }) => (this.pmData = data.aqi));

      fetch("https://covid19.th-stat.com/api/open/today")
         .then((data) => {
            return data.json();
         })
         .then((data) => (this.covidData = data));
   },
   data() {
      return {
         covidData: "",
         pmData: "",
         todayDate: new Date().toLocaleString(),
         restaurantList: [
            { name: "โรงมืด", description: "ราคาถูก, ห้องแอร์" },
            {
               name: "โรงพยาบาลจุฬาฯ",
               description:
                  "ราคาปานกลาง-แพง, หลากหลาย, ห้องแอร์, ใช้ true wallet จ่ายได้, ต้องแลกบัตร",
            },
            {
               name: "มิตรทาว",
               description: "ราคาปานกลาง แต่ของกินน้อย",
            },
            {
               name: "วิศวะ",
               description: "ราคาปานกลาง-แพง, ให้ข้าวเยอะ",
            },
            {
               name: "ครุ",
               description: "แอบไกลนะ, หลากหลาย, ของกินเล่นเยอะ",
            },
            {
               name: "บัญชี",
               description: "ราคาถูก, คนละครึ่งได้ 1 ร้าน, เดินทางใกล้",
            },
            // "โรงมืด (ราคาถูก, ห้องแอร์)",
            // "โรงพยาบาลจุฬาฯ (ราคาปานกลาง-แพง, หลากหลาย, ห้องแอร์, ใช้ true wallet จ่ายได้, ต้องแลกบัตร)",
            // "มิตรทาว (ราคาปานกลาง แต่ของกินน้อย)",
            // "วิศวะ (ราคาปานกลาง-แพง, ให้ข้าวเยอะ)",
            // "ครุ (แอบไกลนะ, หลากหลาย, ของกินเล่นเยอะ)",
            // "บัญชี (ราคาถูก, คนละครึ่งได้ 1 ร้าน, เดินทางใกล้)",
         ],
         whereToEat: "",
      };
   },
   methods: {
      handleRandomRestaurant() {
         const GOTO = this.restaurantList[
            Math.floor(Math.random() * this.restaurantList.length)
         ];
         this.whereToEat = GOTO;
      },
   },
};
</script>

<style scoped>
h2 {
   margin-bottom: 0em !important;
}
.yellow {
   background: yellow !important;
}
.orange {
   background: orange !important;
   color: white !important;
}
.red {
   background: red !important;
   color: white !important;
}
.purple {
   background: #d0c4df !important;
}
.darkpurple {
   background: #824fc2 !important;
}
.green {
   background: lightgreen !important;
}

.pm2 {
   border-radius: 10px;
   background: #d0c4df;
   padding: 8px;
   width: 48%;
   height: 100px;
}

.covid {
   background: #d0c4df;
   border-radius: 10px;
   padding: 8px;
   width: 48%;
   height: 100px;
   /* position: absolute;
   width: 100%;
   top: 10%;
   left: 50%;
   transform: translate(-50%, -50%); */
}
.where {
   margin-top: 1rem;
}
.find-eat {
   position: fixed;
   bottom: 10%;
   left: 50%;
   transform: translate(-50%, -50%);

   width: 90%;
}
#wheretoeat {
   font-size: 40px !important;
   color: #fe5f55;
   transition: 0.5ms;
}
</style>
