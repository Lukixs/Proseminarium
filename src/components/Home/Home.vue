<template>
  <div class="main-wrapped">
    <b-container class="bv-example-row test-wrapper">
      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row"><h1>MySQL</h1></div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row"><h2>Vs</h2></div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row"><h1>Click House</h1></div></b-col
        >
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Wczytaj dane z pliku</p>
              <b-button
                v-if="!loadingMySQL.insertFromFile"
                variant="success"
                @click="mysqlInsertFromFile"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="success" disabled>
                <b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="
                mySQL.insertFromFile != null ||
                  clickHouse.insertFromFile != null
              "
            >
              <span v-if="mySQL.insertFromFile != null"
                >{{ mySQL.insertFromFile }}ms</span
              >
              <span> : </span>
              <span v-if="clickHouse.insertFromFile != null"
                >{{ clickHouse.insertFromFile }}ms</span
              >
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Wczytaj dane z pliku</p>
              <b-button
                variant="success"
                :disabled="isLoading"
                @click="clickHouseInsertFromFile"
                v-if="!loadingClickHouse.insertFromFile"
                >Wykonaj</b-button
              >
              <b-button v-else variant="success" disabled>
                <b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Usuń wszystkie dane z tabeli</p>
              <b-button
                v-if="!loadingMySQL.deleteAll"
                variant="danger"
                @click="mysqlDeleteAllData"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="danger" disabled>
                <b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.deleteAll != null || clickHouse.deleteAll != null"
            >
              <span v-if="mySQL.deleteAll != null"
                >{{ mySQL.deleteAll }}ms</span
              >
              <span> : </span>
              <span v-if="clickHouse.deleteAll != null"
                >{{ clickHouse.deleteAll }}ms</span
              >
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Usuń wszystkie dane z tabeli</p>
              <b-button
                variant="danger"
                :disabled="isLoading"
                @click="clickHouseDeleteAll"
                v-if="!loadingClickHouse.deleteAll"
                >Wykonaj</b-button
              >
              <b-button v-else variant="danger" disabled>
                <b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Wyświetl milion rekordów z tabeli</p>
              <b-button
                v-if="!loadingMySQL.show"
                variant="primary"
                @click="mysqlShowMilion"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled>
                <b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div></div
        ></b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.show != null || clickHouse.show != null"
            >
              <span v-if="mySQL.show != null">{{ mySQL.show }}ms</span>
              <span> : </span>
              <span v-if="clickHouse.show != null"
                >{{ clickHouse.show }}ms</span
              >
            </div>
          </div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Wyświetl milion rekordów z tabeli</p>
              <b-button
                variant="primary"
                :disabled="isLoading"
                @click="clickHouseShowMilion"
                v-if="!loadingClickHouse.show"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled>
                <b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div></div
        ></b-col>
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Wstaw losowe rekordy</p>
              <b-button
                v-if="!loadingMySQL.insert"
                variant="success"
                @click="mysqlInsertRandom"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="success" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.insert != null || clickHouse.insert != null"
            >
              <span v-if="mySQL.insert != null">{{ mySQL.insert }}ms</span>
              <span> : </span>
              <span v-if="clickHouse.insert != null"
                >{{ clickHouse.insert }}ms</span
              >
            </div>
          </div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Wstaw losowe rekordy</p>
              <b-button
                v-if="!loadingClickHouse.insert"
                variant="success"
                @click="clickHouseInsertRandom"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="success" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Usuń losowe rekordy</p>
              <b-button
                v-if="!loadingMySQL.delete"
                variant="danger"
                @click="mysqlDeleteRandom"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="danger" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.delete != null || clickHouse.delete != null"
            >
              <span v-if="mySQL.delete != null">{{ mySQL.delete }}ms</span>
              <span> : </span>
              <span v-if="clickHouse.delete != null"
                >{{ clickHouse.delete }}ms</span
              >
            </div>
          </div></b-col
        >

        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div class="buttonCage">
              <p>Usuń losowe rekordy</p>
              <b-button
                v-if="!loadingClickHouse.delete"
                variant="danger"
                @click="clickHouseDeleteRandom"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="danger" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Zaktualizuj losowy rekord</p>
              <b-button
                v-if="!loadingMySQL.update"
                variant="outline-primary"
                @click="mysqlUpdateRandom"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="outline-primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.update != null || clickHouse.update != null"
            >
              <span v-if="mySQL.update != null">{{ mySQL.update }}ms</span>
              <span> : </span>
              <span v-if="clickHouse.update != null"
                >{{ clickHouse.update }}ms</span
              >
            </div>
          </div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Zaktualizuj losowy rekord</p>
              <b-button
                v-if="!loadingClickHouse.update"
                variant="outline-primary"
                @click="clickHouseUpdateRandom"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="outline-primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Złożone zapytanie SELECT</p>
              <b-button
                v-if="!loadingMySQL.select"
                variant="primary"
                @click="mysqlSelect"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.select != null || clickHouse.select != null"
            >
              <span v-if="mySQL.select != null">{{ mySQL.select }}ms</span>
              <span> : </span>
              <span v-if="clickHouse.select != null"
                >{{ clickHouse.select }}ms</span
              >
            </div>
          </div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Złożone zapytanie SELECT</p>
              <b-button
                v-if="!loadingClickHouse.select"
                variant="primary"
                @click="clickHouseSelect"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Zapytanie SELECT z wykorzystaniem GROUP</p>
              <b-button
                v-if="!loadingMySQL.group"
                variant="primary"
                @click="mysqlGroup"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.group != null || clickHouse.group != null"
            >
              <span v-if="mySQL.group != null">{{ mySQL.group }}ms</span>
              <span> : </span>
              <span v-if="clickHouse.group != null"
                >{{ clickHouse.group }}ms</span
              >
            </div>
          </div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Zapytanie SELECT z wykorzystaniem GROUP</p>
              <b-button
                v-if="!loadingClickHouse.group"
                variant="primary"
                @click="clickHouseGroup"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>

      <hr />

      <b-row>
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Zapytanie SELECT z wykorzystaniem WHERE</p>
              <b-button
                v-if="!loadingMySQL.where"
                variant="primary"
                @click="mysqlWhere"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
        <b-col lg="4" sm="12" class="prosemi-column"
          ><div class="prosemi-row">
            <div
              class="resultCage"
              v-if="mySQL.where != null || clickHouse.where != null"
            >
              <span v-if="mySQL.where != null">{{ mySQL.where }}ms</span>
              <span> : </span>
              <span v-if="clickHouse.where != null"
                >{{ clickHouse.where }}ms</span
              >
            </div>
          </div></b-col
        >
        <b-col lg="4" sm="12" class="prosemi-column">
          <div class="prosemi-row">
            <div class="buttonCage">
              <p>Zapytanie SELECT z wykorzystaniem WHERE</p>
              <b-button
                v-if="!loadingClickHouse.where"
                variant="primary"
                @click="clickHouseWhere"
                :disabled="isLoading"
                >Wykonaj</b-button
              >
              <b-button v-else variant="primary" disabled
                ><b-icon
                  icon="arrow-clockwise"
                  animation="spin"
                  font-scale="1"
                ></b-icon
              ></b-button>
            </div>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      isLoading: false,
      mySQL: {
        insertFromFile: null,
        deleteAll: null,
        show: null,
        insert: null,
        delete: null,
        select: null,
        update: null,
        group: null,
        where: null,
        allAbove: null,
      },
      clickHouse: {
        insertFromFile: null,
        deleteAll: null,
        show: null,
        insert: null,
        delete: null,
        select: null,
        update: null,
        group: null,
        where: null,
        allAbove: null,
      },
      loadingMySQL: {
        insertFromFile: false,
        deleteAll: false,
        show: false,
        insert: false,
        delete: false,
        select: false,
        update: false,
        group: false,
        where: false,
        allAbove: false,
      },
      loadingClickHouse: {
        insertFromFile: false,
        deleteAll: false,
        show: false,
        insert: false,
        delete: false,
        select: false,
        update: false,
        group: false,
        where: false,
        allAbove: false,
      },
    };
  },
  components: {},
  methods: {
    async mysqlDeleteAllData() {
      try {
        this.isLoading = true;
        this.loadingMySQL.deleteAll = true;
        const response = await axios.get(
          "http://localhost:8082/mysql/delete-all-data-in-the-table"
        );

        console.log("Insert files from file!");
        this.mySQL.deleteAll = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.deleteAll = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.deleteAll = false;
        console.log(error);
      }
    },

    async mysqlInsertFromFile() {
      try {
        this.isLoading = true;
        this.loadingMySQL.insertFromFile = true;
        const response = await axios.get(
          "http://localhost:8082/mysql/insert-from-file"
        );

        console.log("Insert files from file!");
        this.mySQL.insertFromFile = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.insertFromFile = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.insertFromFile = false;
        console.log(error);
      }
    },

    async mysqlShowMilion() {
      try {
        this.isLoading = true;
        this.loadingMySQL.show = true;
        const response = await axios.get("http://localhost:8082/mysql/mysql");

        console.log("Create!");
        this.mySQL.show = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.show = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.show = false;
        console.log(error);
      }
    },

    async mysqlInsertRandom() {
      try {
        this.isLoading = true;
        this.loadingMySQL.insert = true;
        const response = await axios.get(
          "http://localhost:8082/mysql/insert-random"
        );

        console.log("Delete!");
        this.mySQL.insert = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.insert = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.insert = false;
        console.log(error);
      }
    },

    async mysqlDeleteRandom() {
      try {
        this.isLoading = true;
        this.loadingMySQL.delete = true;
        const response = await axios.get(
          "http://localhost:8082/mysql/delete-random"
        );

        console.log("Update!");
        this.mySQL.delete = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.delete = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.delete = false;
        console.log(error);
      }
    },

    async mysqlUpdateRandom() {
      try {
        this.isLoading = true;
        this.loadingMySQL.update = true;
        const response = await axios.get(
          "http://localhost:8082/mysql/update-random"
        );

        console.log("Update!");
        this.mySQL.update = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.update = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.update = false;
        console.log(error);
      }
    },

    async mysqlSelect() {
      try {
        this.isLoading = true;
        this.loadingMySQL.select = true;
        const response = await axios.get("http://localhost:8082/mysql/select");

        console.log("Update!");
        this.mySQL.select = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.select = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.select = false;
        console.log(error);
      }
    },

    async mysqlGroup() {
      try {
        this.isLoading = true;
        this.loadingMySQL.group = true;
        const response = await axios.get("http://localhost:8082/mysql/group");

        console.log("Select by GROUP!");
        this.mySQL.group = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.group = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.group = false;
        console.log(error);
      }
    },

    async mysqlWhere() {
      try {
        this.isLoading = true;
        this.loadingMySQL.where = true;
        const response = await axios.get("http://localhost:8082/mysql/where");

        console.log("Select by GROUP!");
        this.mySQL.where = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingMySQL.where = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingMySQL.where = false;
        console.log(error);
      }
    },

    // ==================================================================================

    async clickHouseDeleteAll() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.deleteAll = true;
        const response = await axios.get(
          "http://localhost:8081/click/delete-all-data-in-the-table"
        );

        console.log("Insert files from file");
        this.clickHouse.deleteAll = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.deleteAll = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.deleteAll = false;
        console.log(error);
      }
    },

    async clickHouseInsertFromFile() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.insertFromFile = true;
        const response = await axios.get(
          "http://localhost:8081/click/insert-from-file"
        );

        console.log("Insert files from file");
        this.clickHouse.insertFromFile = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.insertFromFile = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.insertFromFile = false;
        console.log(error);
      }
    },

    async clickHouseShowMilion() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.show = true;
        const response = await axios.get("http://localhost:8081/click/house");

        console.log("Show milion records!");
        this.clickHouse.show = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.show = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.show = false;
        console.log(error);
      }
    },

    async clickHouseInsertRandom() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.insert = true;
        const response = await axios.get(
          "http://localhost:8081/click/insertRandom"
        );

        console.log("Insert random!");
        this.clickHouse.insert = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.insert = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.insert = false;
        console.log(error);
      }
    },

    async clickHouseDeleteRandom() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.delete = true;
        const response = await axios.get(
          "http://localhost:8081/click/delete-random"
        );

        console.log("Delete random!");
        this.clickHouse.delete = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.delete = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.delete = false;
        console.log(error);
      }
    },

    async clickHouseUpdateRandom() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.update = true;
        const response = await axios.get(
          "http://localhost:8081/click/updateRandom"
        );

        console.log("Update Random!");
        this.clickHouse.update = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.update = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.update = false;
        console.log(error);
      }
    },

    async clickHouseSelect() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.select = true;
        const response = await axios.get("http://localhost:8081/click/select");

        console.log("Execute select!");
        this.clickHouse.select = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.select = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.select = false;
        console.log(error);
      }
    },

    async clickHouseGroup() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.group = true;
        const response = await axios.get("http://localhost:8081/click/group");

        console.log("Select WHERE!");
        this.clickHouse.group = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.group = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.group = false;
        console.log(error);
      }
    },

    async clickHouseWhere() {
      try {
        this.isLoading = true;
        this.loadingClickHouse.where = true;
        const response = await axios.get("http://localhost:8081/click/where");

        console.log("Select WHERE!");
        this.clickHouse.where = response.data.czasOpreacji;
        this.isLoading = false;
        this.loadingClickHouse.where = false;
      } catch (error) {
        this.isLoading = false;
        this.loadingClickHouse.where = false;
        console.log(error);
      }
    },
  },
};
</script>

<style>
.landing-page {
  min-width: 1140px;
  position: relative;
}
.bv-example-row {
  /* width: 100%; */
  width: 1000px;
}
p {
  margin-bottom: 5px;
}
.prosemi-column {
  position: relative;
  display: flex;
  flex-direction: column;
}
.prosemi-row {
  flex: 1 1 auto;
  min-height: 1px;
  padding: 1.25rem;
  font-size: 1.4rem;
  text-align: center !important;
}
.button {
  width: 50px;
  height: 50px;
}
.buttonCage {
  padding-bottom: 10px;
}
h2 {
  margin-bottom: 3rem !important;
}
.resultCage {
  text-align: center;
  white-space: nowrap;
  font-size: 2.1rem;
}

.test-wrapper {
  margin-top: 120px;

  /* background: linear-gradient(to bottom, #33ccff 0%, #ff99cc 100%); */
  background: #ffffff;
  box-shadow: 0px 14px 40px;
  padding: 40px 55px 45px 55px;
  border-radius: 15px;
}

.main-wrapped {
  padding-bottom: 100px;
}
</style>
