<template>
  <div>
    <Header />
    <Body />
    <Footer />
  </div>
</template>
<script>
import Header from "./common/Header";
import Footer from "./common/Footer";
import Body from "./Body";
export default {
  name: "Index",
  components: {
    Header,
    Footer,
    Body,
  },
};
</script>
