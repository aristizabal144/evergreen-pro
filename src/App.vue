<template>
  <div id="app">
    <el-row type="flex" justify="space-between" style="padding: 20px">
      <el-col :span="10">
        <div>
          <h1
            style="
              font-size: 50px;
              font-weith: bold;
              color: #409eff;
              margin: 0px;
              margin-top: 20px;
              text-align: start;
            "
          >
            EVERGREEN
            <i class="el-icon-grape"></i>
          </h1>
          <h6 style="font-size: 30px; margin: 0px; text-align: start">
            Production module
          </h6>
        </div>
      </el-col>
      <el-col :span="10">
        <el-button
          type="primary"
          style="width: 100%; margin-top: 20px"
          icon="el-icon-check"
          @click="dialogVisible = true"
          >Create register</el-button
        >
      </el-col>
    </el-row>
    <el-row>
      <el-table :data="data" style="width: 100%">
        <el-table-column label="ID">
          <template slot-scope="scope">
            <i class="el-icon-check"></i>
            <span style="margin-left: 10px">{{ scope.row.id }}</span>
          </template>
        </el-table-column>
        <el-table-column label="Reference">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.reference }}</span>
          </template>
        </el-table-column>
        <el-table-column label="Name">
          <template slot-scope="scope">
            <el-tag style="margin-left: 10px" effect="dark">{{
              scope.row.sownname
            }}</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="Type of sowing">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.sowntype }}</span>
          </template>
        </el-table-column>
        <el-table-column label="Plot">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.plot }}</span>
          </template>
        </el-table-column>
        <el-table-column label="Optimal temperature">
          <template slot-scope="scope">
            <el-tag style="margin-left: 10px" effect="dark" type="danger"
              ><b>{{ scope.row.optimaltemp }}°</b></el-tag
            >
          </template>
        </el-table-column>
      </el-table>
    </el-row>

    <!--dialog create-->
    <el-dialog
      title="Create Sowing"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose"
    >
      <el-row>
        <el-col>
          <p style="text-align: start">Reference:</p>
          <el-input
            placeholder="Enter a reference"
            v-model="form.reference"
          ></el-input>
        </el-col>
      </el-row>
      <el-row>
        <el-col>
          <p style="text-align: start">Name:</p>
          <el-input
            placeholder="Enter a name"
            v-model="form.sownname"
          ></el-input>
        </el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="12">
          <p style="text-align: start">Type:</p>
          <el-select v-model="form.sowntype" placeholder="Select">
            <el-option
              v-for="item in types"
              :key="item.name"
              :label="item.name"
              :value="item.name"
            >
            </el-option>
          </el-select>
        </el-col>
        <el-col :span="12">
          <p style="text-align: start">Plot:</p>
          <el-select v-model="form.plot" placeholder="Select">
            <el-option
              v-for="item in plots"
              :key="item.name"
              :label="item.name"
              :value="item.name"
            >
            </el-option>
          </el-select>
        </el-col>
      </el-row>
      <el-row>
        <el-col>
          <p style="text-align: start">Temperature:</p>
          <el-input-number
            placeholder="Enter a temperature"
            v-model="form.optimaltemp"
            style="width: 100%"
          ></el-input-number>
        </el-col>
      </el-row>
      <el-row>
        <el-col>
          <el-button
            type="primary"
            style="width: 100%; margin-top: 20px"
            icon="el-icon-check"
            @click="submit()"
            >Save Changes</el-button
          >
        </el-col>
      </el-row>
    </el-dialog>
  </div>
</template>

<script>
import Vue from "vue"; // in Vue 2
import axios from "axios";
import VueAxios from "vue-axios";

export default {
  data() {
    return {
      data: [],
      dialogVisible: false,
      types: [{ name: "Fruit" }, { name: "Vegetable" }, { name: "Flowers" }],
      plots: [{ name: "PLOT # 1" }, { name: "PLOT # 2" }, { name: "PLOT # 3" }],
      form: {
        sownname: null,
        reference: null,
        sowntype: null,
        plot: null,
        optimaltemp: null,
      },
    };
  },
  created() {
    axios
      .get(
        "http://ec2-3-15-199-208.us-east-2.compute.amazonaws.com:5000/api/sowns"
      )
      .then((response) => (this.data = response.data));
  },
  methods: {
    async submit() {
      let result = await axios.post(
        "http://ec2-3-15-199-208.us-east-2.compute.amazonaws.com:5000/api/sowns",
        this.form
      );
      console.log(result);
      if (result.status == 200) {
        this.dialogVisible = false;
        axios
          .get(
            "http://ec2-3-15-199-208.us-east-2.compute.amazonaws.com:5000/api/sowns"
          )
          .then((response) => (this.data = response.data));
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
