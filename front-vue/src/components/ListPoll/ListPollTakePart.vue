<template>
  <div class = "ListPollTakePart">
		<a @click="Goto('Home')">Back into Menu</a>
    <br />
    <br />
    <div class="myclass" v-for="(Poll) in ListPollTakePart" :key="Poll.index">
      <PollTakePart :CurrentPoll="Poll" :Id="$route.params.Id" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PollTakePart from "@/components/Poll/PollTakePart.vue";

export default {
  name: "ListPollTakePart",
  data() {
    return {
      ListPollTakePart: {}
    };
  },
  mounted: function() {
    axios
      .get(this.$route.params.Url.ListPoll + `${this.$route.params.Id}`)
      .then(response => {
        this.ListPollTakePart = response.data;
      });
  },
  methods: {
		Goto: function(Path) {
      this.$router.push({
        name: Path,
        params: { Id: this.$route.params.Id }
      });
    },
	},
  components: {
    PollTakePart
  }
};
</script>

<style scoped>
.ListPollTakePart {
	box-sizing: border-box;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  flex: 270px;
  margin: 5px 5px 5px 5px;
}

.myclass {
	margin: 5px 5px 5px 5px;
	justify-content: flex-start;
  border: 4px double black; /* Параметры границы */
  background: #fc3; /* Цвет фона */
  padding: 10px;
  flex-basis: 270px;
  min-height: 270px;
  max-width: 270px;
}
</style>