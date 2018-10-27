<template>
  <v-container>
    <v-layout row wrap> 
      

      <div class="center">
      <v-card id="headCard">
        <v-card-title>
          <h1>Contract Address: </h1>  
          <v-spacer></v-spacer>   
          <h2 class="subheading font-weight-regular">{{address}} </h2> 
         <v-spacer></v-spacer>
        </v-card-title>
      </v-card>
      
      <v-tabs color= indigo accent-3 dark slider-color="red">
      <v-tab  ripple>
       Event : Bid Revealed
      </v-tab>
      <v-tab-item>
      <v-card flat>
          <v-card-text><b>Method Name : </b>unsealBid (bytes32,uint256,bytes32)</v-card-text>
          <v-data-table :headers="headers" :items="events" >
          <template slot="items" slot-scope="props">
            <td># {{ props.item.blockNumber }}</td>
            <td class="text-xs-left"> <b>Owner: </b>{{ props.item.returnValues.owner }}
            <br><b>Topic 1: </b>{{ props.item.raw.topics[1] }}
            <br><b>Topic 2: </b>{{ props.item.raw.topics[2] }}
            <br><b>Value: </b>{{ props.item.returnValues.value }}
            <br><b>Status: </b>{{ props.item.returnValues.status }}</td>
          </template>
        </v-data-table>
      </v-card>
      </v-tab-item>
    </v-tabs>
    </div>
    </v-layout>
  </v-container>
</template>

<script>
  import Web3 from 'web3'
  //checks if metamask is injected if not will use Infura provider
  if (typeof web3 !== 'undefined'){
    web3 = new Web3(web3.currentProvider)
  }else{
     const rpc = "https://mainnet.infura.io/v3/54e0b9ce0c11433f92b1ceb40151c888"
     const web3 = new Web3(rpc)
  }
  const contractAddr = '0x6090A6e47849629b7245Dfa1Ca21D94cd15878Ef'
  const ABI = JSON.parse('[{"constant":false,"inputs":[{"name":"_hash","type":"bytes32"}],"name":"releaseDeed","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_hash","type":"bytes32"}],"name":"getAllowedTime","outputs":[{"name":"timestamp","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"unhashedName","type":"string"}],"name":"invalidateName","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"hash","type":"bytes32"},{"name":"owner","type":"address"},{"name":"value","type":"uint256"},{"name":"salt","type":"bytes32"}],"name":"shaBid","outputs":[{"name":"sealedBid","type":"bytes32"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"bidder","type":"address"},{"name":"seal","type":"bytes32"}],"name":"cancelBid","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_hash","type":"bytes32"}],"name":"entries","outputs":[{"name":"","type":"uint8"},{"name":"","type":"address"},{"name":"","type":"uint256"},{"name":"","type":"uint256"},{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"ens","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_hash","type":"bytes32"},{"name":"_value","type":"uint256"},{"name":"_salt","type":"bytes32"}],"name":"unsealBid","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_hash","type":"bytes32"}],"name":"transferRegistrars","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"},{"name":"","type":"bytes32"}],"name":"sealedBids","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_hash","type":"bytes32"}],"name":"state","outputs":[{"name":"","type":"uint8"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_hash","type":"bytes32"},{"name":"newOwner","type":"address"}],"name":"transfer","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_hash","type":"bytes32"},{"name":"_timestamp","type":"uint256"}],"name":"isAllowed","outputs":[{"name":"allowed","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_hash","type":"bytes32"}],"name":"finalizeAuction","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"registryStarted","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"launchLength","outputs":[{"name":"","type":"uint32"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"sealedBid","type":"bytes32"}],"name":"newBid","outputs":[],"payable":true,"type":"function"},{"constant":false,"inputs":[{"name":"labels","type":"bytes32[]"}],"name":"eraseNode","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_hashes","type":"bytes32[]"}],"name":"startAuctions","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"hash","type":"bytes32"},{"name":"deed","type":"address"},{"name":"registrationDate","type":"uint256"}],"name":"acceptRegistrarTransfer","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_hash","type":"bytes32"}],"name":"startAuction","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"rootNode","outputs":[{"name":"","type":"bytes32"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"hashes","type":"bytes32[]"},{"name":"sealedBid","type":"bytes32"}],"name":"startAuctionsAndBid","outputs":[],"payable":true,"type":"function"},{"inputs":[{"name":"_ens","type":"address"},{"name":"_rootNode","type":"bytes32"},{"name":"_startDate","type":"uint256"}],"payable":false,"type":"constructor"},{"anonymous":false,"inputs":[{"indexed":true,"name":"hash","type":"bytes32"},{"indexed":false,"name":"registrationDate","type":"uint256"}],"name":"AuctionStarted","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"hash","type":"bytes32"},{"indexed":true,"name":"bidder","type":"address"},{"indexed":false,"name":"deposit","type":"uint256"}],"name":"NewBid","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"hash","type":"bytes32"},{"indexed":true,"name":"owner","type":"address"},{"indexed":false,"name":"value","type":"uint256"},{"indexed":false,"name":"status","type":"uint8"}],"name":"BidRevealed","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"hash","type":"bytes32"},{"indexed":true,"name":"owner","type":"address"},{"indexed":false,"name":"value","type":"uint256"},{"indexed":false,"name":"registrationDate","type":"uint256"}],"name":"HashRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"hash","type":"bytes32"},{"indexed":false,"name":"value","type":"uint256"}],"name":"HashReleased","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"hash","type":"bytes32"},{"indexed":true,"name":"name","type":"string"},{"indexed":false,"name":"value","type":"uint256"},{"indexed":false,"name":"registrationDate","type":"uint256"}],"name":"HashInvalidated","type":"event"}]')
  const contract = new web3.eth.Contract(ABI, contractAddr);

  export default {
    data () {
      return {
        
        headers: [
          {
            text: 'Block Number',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'Event Info', align: 'center', sortable: false}
        ],
        events: [],
        address: ''
      }
    },
    mounted(){
      this.address = contract._address
      contract.getPastEvents('BidRevealed', {fromBlock: 6573350, toBlock: 'latest'}, (err, result)=>{
      if(err){
        console.log(err)
      }else{
        console.log(result[1])
         for(var i=0;i<result.length;i++){
          this.events.push(result[i])//push event info to array
         } 
         this.events.reverse() //reverse array to get latest events
         
      }
    })
    web3.eth.getBlockNumber().then(console.log)
    }
  }
</script>

<style>
#heading{
  padding-bottom: 5%;
  color: white;
}
#headCard{
  margin-left: 5%;
  margin-bottom: 5%;
 
}
.center
{
     margin: 0 auto;
}
#grid{
  margin-left: 5%;
  margin-bottom: 5%;
 
}
</style>
