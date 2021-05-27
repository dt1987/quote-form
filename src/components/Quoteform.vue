<template>
  <div class="container">
    <h1 class="mt-4 text-center">Pickup Request</h1>
    <form>
      <div class="row">
        <div class="col-sm-6">

      <div class="form-group">
        <label for="shipto">Ship To</label>
        <textarea
          placeholder="Ship to"
          v-model="shipto"
          class="form-control"
        />
      </div>
    </div>
      <div class="col-sm-6">
      <div class="form-group">
        <label for="sonumber">SO #</label>
        <input
          type="number"
          placeholder="Do not include class"
          v-model="sonumber"
          class="form-control"
        />
      </div>
      </div>
      </div>
      <div class="row">
        <div class="col-sm-4">
          <div class="form-group">
            <label for="length">L</label>
            <input 
              type="number" 
              v-model="pltlength" 
              class="form-control">
          </div>
        </div>
        <div class="col-sm-4">
          <div class="form-group">
            <label for="width">W</label>
            <input 
            type="number" 
            v-model="pltwidth" 
            class="form-control">
          </div>
        </div>
        <div class="col-sm-4">
          <div class="form-group">
            <label for="height">H</label>
            <input type="number" 
            v-model="pltheight" 
            class="form-control">
          </div>
        </div>
      </div>
      <button type="button" @click="onSubmit" class="btn btn-dark" tabindex="0">
        Submit
      </button>
    </form>
    <table class="table mt-5">
      <thead>
        <tr class="table-row">
          <th scope="col">#</th>
          <th scope="col">Ship To</th>
          <th scope="col">SO #</th>
          <th scope="col">L</th>
          <th scope="col">W</th>
          <th scope="col">H</th>
        </tr>
      </thead>
      <tbody>
        <tr class="table-row" v-for="(entry, i) in sortedList" :key="i">
          <th scope="row">{{ ++i }}</th>
          <td id="shipTo" class="table-cell">{{ entry.shipto }}</td>
          <td class="table-cell">{{ entry.sonumber }}</td>
          <td class="table-cell">{{ entry.pltlength }}</td>
          <td class="table-cell">{{ entry.pltwidth }}</td>
          <td class="table-cell">{{ entry.pltheight }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Quoteform",
  data: () => ({ 
    shipto: "", 
    sonumber: "", 
    pltlength: "",
    pltwidth: "",
    pltheight: "", 
    allSonums: [] }),
  computed: {
    sortedList: function() {
      return this.allSonums.slice().sort(function(a, b) {
        return b.sonumber - a.sonumber;
      });
    },
  },
  methods: {
    onSubmit() {
      this.allSonums.push({ 
        shipto: this.shipto, 
        sonumber: this.sonumber,
        pltlength: this.pltlength,
        pltwidth: this.pltwidth,
        pltheight: this.pltheight 
      });
      this.clearForm();
    },
    clearForm() {
      this.shipto = "";
      this.sonumber = "";
      this.pltwidth = "";
      this.pltlength = "";
      this.pltheight = "";
    },
  },
};
</script>
<style scoped>
#shipTo {
white-space:pre-wrap; 
word-wrap:break-word
}
</style>