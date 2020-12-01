<template>
    <form class="createtweetpanel" @submit.prevent="createnewtweet" :class="{'--exceeded': newtweetcharactercount > 240}">
              <label for="newtweet">
                  <strong> New Tweet </strong>{{newtweetcharactercount}}/240
              </label>
              <textarea id="newtweet" rows="4" v-model="newtweetcontent"/>
                <div class="createtweetpanel_submit">
              <div class="createtweettype">
                  <label for="newtweettype"><strong>Type: </strong></label>
                  <select id="newtweettype" v-model="selectedtweettype">
                      <option :value="option.value" v-for="(option,index) in tweetTypes" :key="index">
                          {{option.name}}
                      </option>
                  </select>          
              </div>    
              <button class="button">
                     Tweet
                </button>
                </div>
     </form>
</template>

<script>
export default {
    name: "Createtwitterpanel",
    data(){
    return{

        newtweetcontent:'',
        selectedtweettype:'instant',
        tweetTypes:
            [
                {value:'draft', name: 'Draft'},
                {value:'instant',name: 'Instant Tweet'}
            ],
    
            }},
        computed: {
        newtweetcharactercount(){
          return this.newtweetcontent.length;
        }

         },
     methods: {
      createnewtweet(){
          if(this.newtweetcontent && this.selectedtweettype !== `draft`){
              this.$emit('add-tweet', this.newtweetcontent)
              this.newtweetcontent='';
          }
      }
  }

}
</script>

<style>
.createtweetpanel{
      margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
}
.textarea{
    border: 1px solid #DFE3E8;
    border-radius: 5px;
}
.createtweettype{
    padding: 10px 0;
}
.button{
     padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
}

</style>