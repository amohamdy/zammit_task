<template>
  <router-view/>
</template>

<style lang="scss">
@import "./scss/mixins.scss";

html, body, #app{
  width:100%;
  min-height: 100%;
  margin:0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: gray;
  padding-block:50px;

}
.card{
  border-radius: 11px;
  background-color: white;
  width:75%;
  padding:2.5rem;
  margin:auto;
  margin-bottom:1rem;

  }

  .form-control{
    border:1px solid gray;
    border-radius: 5px;
    width:100%;
    padding:4px 8px;

  }
  .form-group{
    margin-bottom: 1rem;
  }
  .mb-2{
    margin-bottom:0.5rem;
  }
  .mb-4{
    margin-bottom:1.5rem;
  }
  .d-flex{
    @include display-flex(row,flex-start,flex-start);
    flex-wrap: wrap;

  }
  .text-left{
    text-align:left
  }
.flex-column{
  flex-direction: column;
}

.align-items-center{
  align-items: center;
}
.justify-content-start{
  justify-content: flex-start;
}
.justify-content-between{
justify-content: space-between;

}
.ql-snow{
  width:100%;
}
</style>