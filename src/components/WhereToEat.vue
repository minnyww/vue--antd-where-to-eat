<template>
   <div>
      <div class="covid">
         <h3>Covid Update : {{ covidData.UpdateDate }}</h3>
         <h2>ติดเชื่อเพิ่มวันนี้ : {{ covidData.NewConfirmed }}</h2>
         <h2>PM 2.5 : {{ pmData }}</h2>
      </div>
      <div class="where">
         <!-- <em>{{ todayDate }}</em> -->
         <h1>{{ msg }}</h1>
         <h1 id="wheretoeat">{{ whereToEat }}</h1>
         <a-button type="primary" size="large" @click="handleRandomRestaurant"
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
         "http://api.airvisual.com/v2/city?country=Thailand&state=bangkok&city=Pathum%20Wan&key=68039c26-82e0-4afc-8143-53c0b006c21a",
      )
         .then((res) => res.json())
         .then(({ data }) => (this.pmData = data.current.pollution.aqius));

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
            "โรงมืด (ราคาถูก, ห้องแอร์)",
            "โรงพยาบาลจุฬาฯ (ราคาปานกลาง-แพง, หลากหลาย, ห้องแอร์, ใช้ true wallet จ่ายได้, ต้องแลกบัตร)",
            "มิตรทาว (ราคาปานกลาง แต่ของกินน้อย)",
            "วิศวะ (ราคาปานกลาง-แพง, ให้ข้าวเยอะ)",
            "ครุ (แอบไกลนะ, หลากหลาย, ของกินเล่นเยอะ)",
            "บัญชี (ราคาถูก, คนละครึ่งได้ 1 ร้าน, เดินทางใกล้)",
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
.covid {
   position: absolute;
   width: 100%;
   top: 10%;
   left: 50%;
   transform: translate(-50%, -50%);
}
#wheretoeat {
   font-size: 40px !important;
   color: #fe5f55;
   transition: 0.5ms;
}
</style>
