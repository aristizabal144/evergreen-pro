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
              scope.row.name
            }}</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="Type of sowing">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.type }}</span>
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
              ><b>{{ scope.row.temperature }}°</b></el-tag
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
          <el-input placeholder="Enter a reference" v-model="input"></el-input>
        </el-col>
      </el-row>
      <el-row>
        <el-col>
          <p style="text-align: start">Name:</p>
          <el-input placeholder="Enter a name" v-model="input"></el-input>
        </el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="12">
          <p style="text-align: start">Type:</p>
          <el-select v-model="value" placeholder="Select">
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
          <el-select v-model="value" placeholder="Select">
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
          <el-input-number placeholder="Enter a temperature" v-model="input" style="width:100%;"></el-input-number>
        </el-col>
      </el-row>
      <el-row>
        <el-col>
          <el-button
          type="primary"
          style="width: 100%; margin-top: 20px"
          icon="el-icon-check"
          >Save Changes</el-button
        >
        </el-col>
      </el-row>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          id: 1,
          reference: "PRO-1",
          name: "Apple",
          type: "fruits",
          plot: "PLOT #1",
          temperature: 29,
        },
        {
          id: 1,
          reference: "PRO-2",
          name: "Banana",
          type: "fruits",
          plot: "PLOT #2",
          temperature: 21,
        },
        {
          id: 1,
          reference: "PRO-3",
          name: "Berry",
          type: "fruits",
          plot: "PLOT #3",
          temperature: 19,
        },
      ],
      dialogVisible: false,
      types: [
        {name: "Fruit"},
        {name: "Vegetable"},
        {name: "Flowers"}
      ],
      plots: [
        {name: "PLOT # 1"},
        {name: "PLOT # 2"},
        {name: "PLOT # 3"}
      ]
    };
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
