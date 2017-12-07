<template>

<div id="app" class="">
  <nav class="panel">
    <p class="panel-heading">Tasks</p>
  </nav>



  <div class="inputDiv">
    <input class="inputAdd input is-info " id="addTask" type="text" >
    <button class="submitButton button is-link is-outlined" @click="addItem">Submit</button>
  </div>
  <!--<article class="message">!-->
    <div class="column is-half is-offset-one-quarter">
      <div class="message-body taskBody" v-for="task in tasks">
        <input type="checkbox" id="checkbox" class="checkbox" @click="updateStatus(task.id)"  :checked="task.completed"> 
        <p><strong>Task: {{task.title}}</strong></p>
        <tr>
          <td>
            <p> Created: {{task.created}}</p>
            <p> Updated: {{task.updated}}</p>
          </td>
        </tr> 
      </div>
    </div>
  <!--</article>!-->  
  </div>


</template>



<script>
import axios from 'axios';
export default {
  name: 'app',
  data () {
    return {
    tasks:[] 
    };
  },
  computed:{

  },
  methods:{

    updateStatus: function(id) {
      console.log(id)

      axios.post('http://fjolbraut.org/api/tasks/' + id + '/status?api_token=mrIVOC9IQquYCqp2RXN90PeASlhRwZdQoXxqnilpCuavlCZomKS6nYV8WUPv')
        .then(function(response) {
            console.log(response);
        })
        .catch(function(error) {
            console.log(error);
         });
    },


      addItem: function() {
        var valInput= document.getElementById("addTask").value
        axios.post('http://fjolbraut.org/api/tasks?api_token=mrIVOC9IQquYCqp2RXN90PeASlhRwZdQoXxqnilpCuavlCZomKS6nYV8WUPv', {
          title: valInput
        })
          .then(function(response) {
            console.log(response);
          })
          .catch(function(error) {
            console.log(error);
          });
        },


  },

  
  mounted(){
    var self = this;
      axios.get('http://fjolbraut.org/api/tasks?api_token=mrIVOC9IQquYCqp2RXN90PeASlhRwZdQoXxqnilpCuavlCZomKS6nYV8WUPv')
           .then(function(response) {
              self.tasks = response.data
           }).
           catch(function(error) {
              console.log(error);
           });


  }
}
</script>
<style>
  .inputDiv {
    text-align: center;
    margin-left: 40%;
    margin-right: 40%;
    margin-top: 80px;
  };

  .checkbox:checked {
    text-decoration: overline; 
  };

  .taskBody {
    margin:10px;
    display:inline-block;
  };

</style>
