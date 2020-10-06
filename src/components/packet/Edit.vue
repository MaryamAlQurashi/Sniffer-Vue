<template>
  <div>
    <h4 class="text-center mt-20">
    <small>
    <button class="btn btn-success" v-on:click="navigate()"> View All Packets </button>
    </small>
    </h4>


        <div class="col-md-12 form-wrapper">  
          <h2> Edit Packet </h2>

            <form id="create-post-form" @submit.prevent="editPacket">


        <div class="form-group col-md-12">
          <label for="title"> TIME </label>
          <input type="text" id="TIME" v-model="packet.TIME" name="title" class="form-control" placeholder="Enter TIME">
        </div>

                
        <div class="form-group col-md-12">
          <label for="title"> IP_SRC </label>
          <input type="text" id="IP_SRC" v-model="packet.IP_SRC" name="title" class="form-control" placeholder="Enter IP_SRC">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> IP_DST </label>
          <input type="text" id="IP_DST" v-model="packet.IP_DST" name="title" class="form-control" placeholder="Enter IP_DST">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> SRC_PORT </label>
          <input type="text" id="SRC_PORT" v-model="packet.SRC_PORT" name="title" class="form-control" placeholder="Enter SRC_PORT">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> SRC_DST </label>
          <input type="text" id="SRC_DST" v-model="packet.SRC_DST" name="title" class="form-control" placeholder="Enter SRC_DST">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> TTL </label>
          <input type="text" id="TTL" v-model="packet.TTL" name="title" class="form-control" placeholder="Enter TTL">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> PROTOCOL </label>
          <input type="text" id="PROTOCOL" v-model="packet.PROTOCOL" name="title" class="form-control" placeholder="Enter PROTOCOL">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> HTTP_VRS </label>
          <input type="text" id="HTTP_VRS" v-model="packet.HTTP_VRS" name="title" class="form-control" placeholder="Enter HTTP_VRS">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> HTTP_VRQ </label>
          <input type="text" id="HTTP_VRQ" v-model="packet.HTTP_VRQ" name="title" class="form-control" placeholder="Enter HTTP_VRQ">
        </div>
        

        <div class="form-group col-md-12">
          <label for="title"> STATUS_CODE </label>
          <input type="text" id="STATUS_CODE" v-model="packet.STATUS_CODE" name="title" class="form-control" placeholder="Enter STATUS_CODE">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> REASON_PH </label>
          <input type="text" id="REASON_PH" v-model="packet.REASON_PH" name="title" class="form-control" placeholder="Enter REASON_PH">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> CONT_LEN_RS </label>
          <input type="text" id="CONT_LEN_RS" v-model="packet.CONT_LEN_RS" name="title" class="form-control" placeholder="Enter CONT_LEN_RS">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> CONT_LEN_RQ </label>
          <input type="text" id="CONT_LEN_RQ" v-model="packet.CONT_LEN_RQ" name="title" class="form-control" placeholder="Enter CONT_LEN_RQ">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> CONT_TYPE_RS </label>
          <input type="text" id="CONT_TYPE_RS" v-model="packet.CONT_TYPE_RS" name="title" class="form-control" placeholder="Enter CONT_TYPE_RS">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> CONT_TYPE_RQ </label>
          <input type="text" id="CONT_TYPE_RQ" v-model="packet.CONT_TYPE_RQ" name="title" class="form-control" placeholder="Enter CONT_TYPE_RQ">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> URL </label>
          <input type="text" id="URL" v-model="packet.URL" name="title" class="form-control" placeholder="Enter URL">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> METHOD </label>
          <input type="text" id="METHOD" v-model="packet.METHOD" name="title" class="form-control" placeholder="Enter METHOD">
        </div>


        <div class="form-group col-md-12">
          <label for="title"> PAYLOAD </label>
          <input type="text" id="PAYLOAD" v-model="packet.PAYLOAD" name="title" class="form-control" placeholder="Enter PAYLOAD">
        </div>


        <div class="form-group col-md-4 pull-right">
          <button class="btn btn-success" type="submit"> Edit Packet </button>
        </div>  


          </form>
        </div>
    </div>
</template>


<script>
import { server } from "../../helper";
import axios from "axios";
import router from "../../router";
export default {
  data() {
    return {
      id: 0,
      packet: {}
    };
  },
  created() {
    this.id = this.$route.params.id;
    this.getPacket();
  },
  methods: {
    editPacket() {
      let packetData = {
        TIME: this.TIME,
        IP_SRC: this.IP_SRC,
        IP_DST: this.IP_DST,
        SRC_PORT: this.SRC_PORT,
        DST_PORT: this.DST_PORT,
        TTL: this.TTL,
        PROTOCOL: this.PROTOCOL,
        HTTP_VRS: this.HTTP_VRS,
        HTTP_VRQ: this.HTTP_VRQ,
        STATUS_CODE: this.STATUS_CODE,
        REASON_PH: this.REASON_PH,
        CONT_LEN_RS: this.CONT_LEN_RS,
        CONT_LEN_RQ: this.CONT_TYPE_RQ,
        CONT_TYPE_RS: this.CONT_TYPE_RS,
        CONT_TYPE_RQ: this.CONT_TYPE_RQ,
        URL: this.URL,
        METHOD: this.METHOD,
        PAYLOAD: this.PAYLOAD
      };
      axios
        .put(
          `${server.baseURL}/packet/update?packetID=${this.id}`,
          packetData
        )
        .then(function() {
          router.push({ name: "home" });
        });
    },
    getPacket() {
      axios
        .get(`${server.baseURL}/packet/packet/${this.id}`)
        .then (function() { (this.packet = data.data) } );
    },
    navigate() {
      router.go(-1);
    }
  }
};
</script>