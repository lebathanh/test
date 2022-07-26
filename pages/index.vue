<template>
  <v-row justify="center" align="center">
    <v-col cols="12" class="inp_show">
      <h2>{{ result }}</h2>
    </v-col>
    <v-col cols="9">
      <v-row>
        <v-col v-for="item in getKeyNums" :key="item.key" cols="4">
          <v-btn block @click="result += item.key">
            {{ item.key }}
          </v-btn>
        </v-col>
      </v-row>
    </v-col>
    <v-col cols="3">
      <v-row>
        <v-col v-for="item in getKeyExcs" :key="item.key" cols="12">
          <v-btn block @click="excCal($event, item.key)">
            {{ item.key }}
          </v-btn>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      result: "",
      btns: [
        {
          key: 0,
          type: "Num",
        },
        {
          key: 1,
          type: "Num",
        },
        {
          key: 2,
          type: "Num",
        },
        {
          key: 3,
          type: "Num",
        },
        {
          key: 4,
          type: "Num",
        },
        {
          key: 5,
          type: "Num",
        },
        {
          key: 6,
          type: "Num",
        },
        {
          key: 7,
          type: "Num",
        },
        {
          key: 8,
          type: "Num",
        },
        {
          key: 9,
          type: "Num",
        },
        {
          key: "C",
          type: "EXC",
        },
        {
          key: "CE",
          type: "EXC",
        },
        {
          key: "+",
          type: "EXC",
        },
        {
          key: "-",
          type: "EXC",
        },
        {
          key: "*",
          type: "EXC",
        },
        {
          key: "/",
          type: "EXC",
        },
        {
          key: "=",
          type: "EXC",
        },
      ],
    };
  },

  computed: {
    getKeyNums(ctx) {
      return ctx.btns.filter((btn) => btn.type === "Num");
    },
    getKeyExcs(ctx) {
      return ctx.btns.filter((btn) => btn.type === "EXC");
    },
  },

  methods: {
    excCal(e, type) {
      const exc = ["+", "-", "*", "/"];
      switch (type) {
        case "C":
          this.result = "";
          break;
        case "CE":
          this.result = this.result.substring(0, this.result.length - 1);
          break;
        case "=":
          if (!exc.includes(this.result.slice(-1))) {
            this.result = eval(this.result).toString();
          }
          break;
        default:
          const addExc = () => {
            if (exc.includes(this.result.slice(-1))) {
              this.result =
                this.result.substring(0, this.result.length - 1) + type;
            } else {
              this.result += type;
            }
          };
          if (this.result.length >= 2) {
            addExc();
          } else {
            if (type === "+" || type === "-") {
              addExc();
            }
          }
          break;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.inp_show {
  height: 60px;
  margin: 12px;
  padding: 12px;
  border: 1px solid white;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  flex-direction: column;
}
</style>
