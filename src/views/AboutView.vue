<template>
  <div>
    <HeaderCont />
    <TitleCont name1="about" name2="me" />
    <SectionCont />
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import SectionCont from "@/components/SectionCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    SectionCont,
    TitleCont,
    ContactCont,
  },
};
</script>
