<template>
  <div>
    <table id="currencies">
      <thead>
        <td>FROM/TO</td>
        <td>DIFFERENCE</td>
        <td></td>
      </thead>
      <tbody>
        <tr>
          <td>Poloniex/HitBTC</td>
          <td>{{ PLNX_TO_HBTC }}</td>
          <td v-if="PLNX_TO_HBTC > PLNX_TO_HBTC_OLD">
            <img src="../../static/up.png">
          </td>
          <td v-else>
            <img src="../../static/down.png">
          </td>
        </tr>
        <tr>
          <td>HitBTC/Poloniex</td>
          <td>{{ HBTC_TO_PLNX }}</td>
          <td v-if="HBTC_TO_PLNX > HBTC_TO_PLNX_OLD">
            <img src="../../static/up.png">
          </td>
          <td v-else>
            <img src="../../static/down.png">
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

  export default {
    name: 'home',
    data() {
      return {
        HBTC_TO_PLNX: 0,
        PLNX_TO_HBTC: 0,
        HBTC_TO_PLNX_OLD: 0,
        PLNX_TO_HBTC_OLD: 0,
      }
    },
    methods: {
      fetchData() {
        let _this = this;
        this.$http.get('http://localhost:8085/api/data/getPlnxToHbtc')
          .then(function (response) {
            _this.PLNX_TO_HBTC = response.data;
            if (HBTC_TO_PLNX_OLD != 0) {
              HBTC_TO_PLNX_OLD = response.data;
            }
          });

          this.$http.get('http://localhost:8085/api/data/getHbtcToPlnx')
          .then(function (response) {
            _this.HBTC_TO_PLNX = response.data;
            if (PLNX_TO_HBTC_OLD != 0) {
              PLNX_TO_HBTC_OLD = response.data;
            }
          });
      },
    },
    created() {
      let _this = this;
      setInterval(function () {
        _this.fetchData();
      }, 1000);
    }
  }
</script>

<style scoped>
  #currencies {
    font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
    border-collapse: collapse;
    width: 100%;
    text-align: center;
}

#currencies td, #currencies th {
    border: 1px solid #ddd;
    padding: 8px;
}

#currencies tr:nth-child(even){background-color: #f2f2f2;}

#currencies tr:hover {background-color: #ddd;}

#currencies th {
    padding-top: 12px;
    padding-bottom: 12px;
    text-align: left;
    background-color: #4CAF50;
    color: white;
}

img {
  max-width: 20px;
}
</style>
