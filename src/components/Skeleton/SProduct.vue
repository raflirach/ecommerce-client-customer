<template>
  <div class="card col-2 m-1">
    <div id="box" class="shine"></div>
    <div class="px-2">
      <div id="lines" class="title shine"></div>
      <div class="footer">
        <div id="lines" class="price shine"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
  .card{
    padding: 0 !important;
    height: 280px;
    border: 1px solid #e3e3e3;
  }
  .footer{
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    bottom: 0;
    width: 100%;
    padding-left: 2px;
    padding-bottom: 2px;
  }
  .price{
    height: 15px;
    width: 50% !important;
  }
  #lines {
    height: 15px;
    margin-top: 10px;
    width: 100%;
  }
  #box {
    height: 200px;
    width: 100%;
  }
</style>
