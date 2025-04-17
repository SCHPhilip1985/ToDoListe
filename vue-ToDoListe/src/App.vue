<script setup>
import { ref } from "vue"

const toDoList = ref(JSON.parse(localStorage.getItem("ToDo - Liste")) || [])
const toDoItem = ref({done:false})
// toDoItem soll alle elemente aus Eingabe aufnehmen
// toDoItem = {Nr:0, Aufgaben:"Aufgaben", Ausführender:"Ausführender", }

const inputOpen = ref(false)
const isNew = ref(true)


function addToList() {
  toDoList.value.push(JSON.parse(JSON.stringify(toDoItem.value)))
  localStorage.setItem("ToDo - Liste", JSON.stringify(toDoList.value))
}

function storeChanges() {
  localStorage.setItem("ToDo - Liste", JSON.stringify(toDoList.value))
}

function editEntry(Index) {
isNew.value = false
toDoItem.value = toDoList.value[Index]
inputOpen.value = true
}

function deleteFromList(Index) {
  toDoList.value.splice(Index, 1)
}


</script>text

<template>
  <input type="checkbox" v-model="inputOpen">
  {{ inputOpen }}
  <h1>ToDo - Liste</h1>
<form v-if="inputOpen">

  <p>Nr. #</p>
  <input type="number" placeholder="Nr." v-model="toDoItem.nr">
  
  <p>Aufgaben</p>
  <input type="text" placeholder="Zu erledigende Aufgaben" v-model="toDoItem.task"> 
  
  <p>Person
    <select v-model="toDoItem.person">
      <option value="Philip">Philip</option>
      <option value="Carlos">Carlos</option>
      <option value="Jofi">Jofi</option>
    </select> 
  </p>
  
  <p>
    <input type="date" placeholder="Datum" v-model="toDoItem.date">
  </p>
  
  <p>Tageszeit
    <select v-model="toDoItem.daytime">
      <option value="Morgens">Morgens</option>
      <option value="Mittags">Mittags</option>
      <option value="Abends">Abends</option>
    </select>
  </p>
  
  <p>Erledigt?</p>
  <input type="checkbox" v-model="toDoItem.done">
    
  <button v-if="isNew" @click="addToList()">Zur Liste Hinzufügen</button>
  <button v-else @click="storeChanges()">Ändern</button>
</form>
<button v-else @click="inputOpen=true">New</button>
 
  <!-- {{ toDoItem }} -->
  <hr>
  <section class="listHeader">
    <div>Nr.</div>
    <div>Aufgabe</div>
    <div>Person</div>
    <div>Datum</div>
    <div>Tageszeit</div>
    <div>Erledigt?</div>
    <div>Ändern</div>
    <div>Löschen</div>

  </section>
  <section class="oneListItem" v-for="(toDo, Index) in toDoList">
    <div>{{ toDo.nr }}</div>
    <div>{{ toDo.task }}</div>
    <div>{{ toDo.person }}</div>
    <div>{{ toDo.date }}</div>
    <div>{{ toDo.daytime }}</div>
    <div>{{ toDo.done }}</div>
    <button @click="editEntry(Index)">Änderungen</button>
    <button @click="deleteFromList(Index)">Löschen</button>
  
  </section>

  
  




  
</template>

<style>

body {
  font-family: Arial, Helvetica, sans-serif;
  font-size: larger;
  color: darkblue;
}

.listHeader {
  display: flex;
  justify-content: space-between;
  padding:5px;
  margin:10px auto;
  width: 90%;
}

.oneListItem{
    padding:5px;
    margin:10px auto;
    box-shadow: 0 0 3px grey;
    border-radius: 5px;
    width: 90%;
    transition: all 0.5s;
    display: flex;
    justify-content: space-between;
  }



</style>
