<template>
  <div class="">
    <span class="heading display-table">Bookshelf & </span>
    <span class="heading display-table"> Book Racks</span>

    <p class="description text-start">
      Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum is simply dummy text of the
      printing and typesetting industry. Lorem Ipsum is simply dummy text of the printing and typesetting industry.
    </p>

  </div>

</template>


<script>
export default {
  name: 'background-compo',
  data() {
    return {
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.heading{
  font-size: 64px;
    font-weight : inherit;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.125;
    letter-spacing: normal;
    color: #fff;
    /* padding-left: 50px; */
    margin: 0 0 16px;
    text-align: left;
}
.display-table{
  display: flex;
}

.description{
  font-family: Helvetica Neue LT W05_45 Light;
    font-size: 16px;
    font-weight: lighter;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.38;
    letter-spacing: .4px;
    color: #fff;
    margin: 0;
    max-width: 460px;
    /* padding-left: 50px; */
}
.text-start{
  text-align: start;
}

/* Responsive columns - one column layout (vertical) on small screens */
@media screen and (max-width: 600px) {
  .heading {
    font-size: 32px;
  }
}
</style>
