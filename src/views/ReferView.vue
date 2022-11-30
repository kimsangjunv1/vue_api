<template>
  <div>
    <HeaderCont />
    <TitleCont name1="reference" name2="api" />
    <section className="cont__refer">
      <div className="container">
        <div className="refer__inner">
          <h2>CSS</h2>
          <ul className="refer__list">
            <li v-for="refer in refers" :key="refer.title">
              <span class="num">{{ refer.num }}</span>
              <span class="desc">{{ refer.title }}</span>
              <span>{{ refer.desc }}</span>
              <span>{{ refer.descApple }}</span>
              <span>{{ refer.descVer }}</span>
              <span class="star">{{ refer.descStar }}</span>
            </li>
          </ul>
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },

  setup() {
    const refers = ref([]);

    const references = () => {
      fetch(
        "https://raw.githubusercontent.com/kimsangjunv1/react_api/main/src/utis/reference.json"
      )
        .then((response) => response.json())
        .then((result) => (refers.value = result.cssReference))
        // .then((result) => console.log(result.cssReference))
        .catch((error) => console.log("error", error));
    };
    references();

    return {
      refers,
      references,
    };
  },
};
</script>

<style lang="scss">
.refer__inner {
  padding-bottom: 200px;

  h2 {
    font-size: 30px;
    color: var(--dark);
  }
}

.refer__list {
  border: 1px solid var(--bg-dark-border);
  // border-top-width: 2px;

  li {
    border-bottom: 1px solid var(--bg-dark-border);
    padding: 10px;
    color: #fff;
    position: relative;
    span {
      display: block;
      padding-left: 10px;
      color: #000;

      &:nth-child(1) {
        position: absolute;
        right: 20px;
        top: 15px;
      }

      &:nth-child(2) {
        font-size: 30px;
        border-bottom: 1px solid var(--bg-dark-border);
        padding-left: 10px;
        margin-bottom: 20px;
      }
      &:nth-child(5) {
        position: absolute;
        top: 15px;
        right: 40px;
        // background: #fff;
        // color: #000;
        border-right: 1px solid var(--bg-dark-border);
        padding-right: 10px;
      }
    }
    a {
      display: flex;
      align-items: center;
      width: 100%;
      color: var(--white);
      // padding: 10px;

      span {
        display: inline-block;
        padding: 15px 20px;
        color: #fff;
        margin-bottom: 10px;

        &:last-child {
          margin-bottom: 0px;
        }
      }

      .num {
        flex: 1 1 5%;
        text-align: center;
        border-right: 1px solid var(--bg-dark-border);
      }
      .name {
        flex: 1 1 20%;
        border-right: 1px solid var(--bg-dark-border);
      }
      .desc {
        flex: 1 1 65%;
        border-right: 1px solid var(--bg-dark-border);
      }
      .star {
        flex: 1 1 10%;
        text-align: center;
      }
    }
  }
}
</style>
