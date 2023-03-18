<template>
  <div class="card-man">
    <a href="http://alqurain.org" target="_blank"
      ><img src="@/assets/logo.png" class="logo"
    /></a>
    <div class="frame">
      <img src="@/assets/imgs/3.png" />
      <img src="@/assets/imgs/4.png" />
    </div>

    <div class="content" v-if="item">
      <div class="photo-handler">
        <img :src="'https://test.api.v1.alqurain.org/' + item.groom_picture" />
      </div>
      <div class="card-content">
        <div class="special-invite">
          <img src="@/assets/imgs/1.png" />
        </div>
        <div class="family">
          <p>أفراح/</p>
          <p class="family-name">{{ item.groom_family }}</p>

          <p v-if="!item.one_family" class="and">
            <img src="@/assets/imgs/9.png" />
          </p>
          <p v-if="!item.one_family" class="family-name">
            {{ item.bride_family }}
          </p>
        </div>
        <p>يشرفنا دعوتكم لحضور مراسم حفل زفاف الفارس</p>
        <p class="married">
          <span>{{ item.groom_name }}</span>
          <span> على </span>
          <span>كريمة {{ item.bride_name }}</span>
        </p>
        <div></div>
        <p>وذلك بمشيئة الله تعالى:</p>
        <div class="info">
          <div class="box">
            <div class="info-img-handler">
              <img src="@/assets/imgs/6.png" />
            </div>
            <div>
              <p>{{ item.day }} {{ item.hijri_date }} هـ - {{ item.date }} م</p>
            </div>
          </div>
          <a :href="item.place_url" class="box" target="_BLANK">
            <div class="info-img-handler">
              <img src="@/assets/imgs/5.png" />
            </div>
            <div>
              <p>{{ item.place }}</p>
            </div>
          </a>
        </div>
        <div>
          <img src="@/assets/imgs/2.png" />
        </div>
        <div class="invite-by">
          <h3>الداعون /</h3>
          <div>
            <p v-for="(inv, id) in item.inviters" :key="id">{{ inv }}</p>
          </div>
        </div>
      </div>
    </div>
    <footer>
      <a href="https://alqurain.org">مهرجان الزواج الجماعي بالقرين</a>
      <ul>
        <li>
          <a href="https://t.me/mahrjanqurain"
            ><img src="@/assets/icons/telegram.svg" alt=""
          /></a>
        </li>
        <li>
          <a href="https://www.snapchat.com/add/mahrjan.qurain"
            ><img src="@/assets/icons/snapchat.svg" alt=""
          /></a>
        </li>
        <li>
          <a href="https://www.instagram.com/mahrjanqurain/"
            ><img src="@/assets/icons/instagram.svg" alt=""
          /></a>
        </li>
        <li>
          <a href="https://www.youtube.com/@mahrjanqurain"
            ><img src="@/assets/icons/youtube.svg" alt=""
          /></a>
        </li>
        <li>
          <a href="https://wa.me/966582566996"
            ><img src="@/assets/icons/whatsapp.svg" alt=""
          /></a>
        </li>
      </ul>
    </footer>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "IndexPage",

  data: function () {
    return {
      title: "gg",
      items: null,
      item: null,
    };
  },
  async fetch() {
    let { data } = await axios.get(
      `https://test.api.v1.alqurain.org/invitations/m/${this.$route.params.id}`
    );
    // if (data.status !== 200) {
    //   this.$router.push("/");
    // }
    this.items = data;
    this.item = this.items.payload;
    // if (items.status !== 200) {
    //   this.$router.push("/error");
    // }
    console.log(this.item);
  },
  // methods: {
  //   async getData() {
  //     const res = await fetch(
  //       `https://test.api.v1.alqurain.org/invitations/m/ali50` //${this.$route.params.id}
  //     );
  //     const finalRes = await res.json();
  //     if (res.status !== 200) {
  //       this.$router.push("/error");
  //     }
  //     this.items = finalRes;
  //     this.item = finalRes.payload;
  //     if (this.item.place === null) {
  //       this.item.place =
  //         "مقر الزواج الجماعي بالقرين بجانب مدرسة ثانوية القرين للبنين";
  //     }
  //     if (this.item.place_url === null) {
  //       this.item.place_url = "https://goo.gl/maps/uHt4UsceWDmTp85BA";
  //     }
  //     this.item.date = this.item.date.split("T")[0];
  //     console.log(this.items);
  //   },
  // },
  // mounted() {
  //   this.getData();
  // },
  head() {
  //       <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
  // <link href=" /img/favicon.png" rel="icon">
  // <link href="/img/apple-touch-icon.png" rel="apple-touch-icon">
  //   <!-- Favicon -->
  //   <link href="img/favicon.ico" rel="icon" />



    return {
      title: `أفراح ${this.item.groom_family} ${
        this.item.one_family ? "" : `و ${this.item.bride_family}`
      }`,
      meta: [
        { hid: "og-type", property: "og:type", content: "website" },
        {
          hid: "description",
          property: "description",
          content: `يشرفنا دعوتكم لحضور مراسم حفل زفاف الفارس ${this.item.groom_name} على كريمة ${this.item.bride_name}`,
        },
        {
          hid: "apple-touch-icon",
          property: "apple-touch-icon",
          rel: "apple-touch-icon",
          content: `https://test.api.v1.alqurain.org/${this.item.groom_picture}`,
        },
        {
          hid: "favicon",
          property: "favicon",
        rel: "icon",
        type:"image/x-icon",
          content: `https://test.api.v1.alqurain.org/${this.item.groom_picture}`,
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
$gold: #b18f31;
$purple: #5e5875;

@font-face {
  font-family: ad-rsail;
  src: url("@/assets/fonts/ad-rsail.ttf");
}
a {
  text-decoration: none;
}
* {
  direction: rtl;
  box-sizing: border-box;
}
.logo {
  z-index: 1000;
  position: fixed;
  left: 30px;
  width: 125px;
  bottom: 45px;
}
.card-man {
  font-family: "ad-rsail";
  width: 100%;
  min-height: 100vh;
  position: relative;
}

.frame img {
  position: fixed;
  max-width: 160px;
  z-index: 10;
}

.frame img:first-child {
  top: 0;
  left: 0;
}

.frame img:last-child {
  bottom: 0;
  right: 0;
}
.content {
  padding: 50px;
  padding-bottom: 0;
  display: flex;
  flex-direction: row;
  .photo-handler {
    display: flex;
    justify-content: center;
    align-content: center;
    align-items: center;
    position: absolute;
    right: 50px;
  }
  .photo-handler img {
    width: 300px;
    height: 300px;
    box-shadow: 1px 1px 15px rgba(0, 0, 0, 0.5);
    border-radius: 50%;

    &:first-child {
      border: solid #443d5f 7px;
    }
  }

  .card-content {
    flex: 1;
    text-align: center;

    display: flex;
    align-content: center;
    flex-direction: column;
    .special-invite {
      width: 250px;
      img {
        width: 100%;
      }
      margin: 0 auto;
    }

    .family {
      direction: rtl;
      margin-top: 50px;
      font-size: 35px;
      color: $gold;
      + p {
        color: $purple;
        font-size: 20px;
        margin: 30px 0;
      }
      p {
        direction: rtl;
        display: inline-block;
      }
      :first-child {
        margin-left: 15px;
      }
      .and img {
        padding: 0 15px;
        vertical-align: middle;
        width: 80px;

        position: relative;
        top: -2px;
      }
      .family-name {
        color: $purple;
        font-weight: bold;
      }
    }

    .married {
      font-size: 30px;
      font-weight: bold;
      color: $purple;
      span:nth-child(2) {
        color: $gold;
        margin: 10px;
      }
      + div {
        background: $gold;
        width: 250px;
        margin: 30px auto;
        height: 3px;
        + p {
          color: $purple;
          font-size: 30px;
        }
      }
    }

    .info {
      display: flex;
      justify-content: center;
      align-items: center;
      line-height: 1.5;
      .box {
        display: flex;
        align-items: center;
        justify-content: center;
        color: $purple;
        margin-top: 30px;
        font-size: 18px;
        .info-img-handler {
          width: 50px;
          margin: 10px;
        }
        img {
          width: 100%;
        }
      }
      + div {
        margin: 5px auto;
        width: 450px;
        img {
          width: 100%;
        }
      }
    }
  }
  .invite-by {
    margin-top: 25px;
    margin-bottom: 70px;
    h3 {
      font-size: 25px;
      color: $gold;
      font-weight: normal;
    }
    div {
      color: $purple;
      margin-top: 10px;
      line-height: 1.8;
      font-weight: bold;

      display: flex;
      flex-direction: column;
      p {
        margin: 0 20px !important;
        font-size: 15px;
      }
    }
  }
}
footer {
  margin-top: 10px;
  width: 100%;
  background: #5e5875;
  text-align: center;
  padding: 20px;
  color: white;
  a {
    text-decoration: none;
    color: #fff;
  }
  ul {
    display: flex;
    flex-direction: row-reverse;
    align-items: center;
    justify-content: center;
    list-style: none;
    img {
      width: 30px;
      margin: 10px 5px 0;
    }
  }
}

@media (max-width: 1450px) {
  .photo-handler img {
    width: 240px;
    width: 240px;
    border-width: 5px !important;
  }
  .content {
    flex-direction: column;
  }
  .photo-handler {
    margin-bottom: 14px;
    position: relative !important;
    right: 0 !important;
  }

  .frame img {
    width: 150px;
  }
  .special-invite {
    width: 140px !important;
  }
  .family {
    margin-top: 10px !important;
    .and img {
      width: 70px !important;
      margin-left: 0 !important;
    }
    + p {
      margin: 20px !important;
    }
  }

  .married {
    font-size: 24px !important;
    + div {
      margin: 15px auto !important;
    }
  }
  .info .box {
    margin: 10px !important;
  }
}

@media (min-width: 1450px) {
  .invite-by {
    div {
      width: 30%;
      margin-left: auto;
      margin-right: auto;
    }
  }
  .invite-by {
  }
}
@media (max-width: 1050px) {
  .married {
    font-size: 20px !important;
    display: flex;
    flex-direction: column;

    + div {
      margin: 15px auto !important;
      + * {
        font-size: 22px !important;
      }
    }
  }
}
@media (max-width: 767px) {
  .logo {
    width: 90px;
    top: 10px;
    left: unset;
    right: 10px !important;
    z-index: 9999;
  }
  .photo-handler img {
    width: 170px !important;
    height: 170px !important;

    border: solid #443d5f 3px !important;
  }

  .content {
    padding: 10px;
  }

  .frame img {
    width: 60px;
  }
  .special-invite {
    width: 100px !important;
  }
  .family {
    p {
      font-size: 20px;
    }
    p.family-name {
      font-size: 20px !important;
    }
    .and img {
      width: 55px !important;
    }
    + p {
      font-size: 18px !important;
    }
  }
  .invite-by {
    margin-bottom: 25px !important;
  }

  .info .box {
    flex-direction: column !important;
    .info-img-handler {
      width: 30px !important;
      flex-basis: 50% !important;
    }

    p {
      font-size: 12px !important;
      font-weight: bold;
    }
  }
  .info + div {
    width: 250px !important;
    margin: 0 auto !important;
  }
}
/* @media (min-height: 876px) and (min-width: 387px) {
  footer {
    position: absolute !important;
  }
 } */
</style>
