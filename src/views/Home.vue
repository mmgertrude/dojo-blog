<template>
  <div class="home">
    <p>This is the home page</p>
    <h2> Refs demo:</h2>
  
    <!--<p ref ="p">my name is {{nameNotReactive}} and my age is {{ageNotReactive}}</p>
    <p ref ="para">my name is {{name}} and my age is {{age}}</p>
     -->
    <p>{{ninjaOne.name}} {{ninjaOne.age}} </p>
    <button @click="updateNinjaOne">Update ninja one</button>
  <!--
    <button @click="handleClick">Click me</button>
    <button @click="age++">Add 1 to age</button>
    <input type="text" v-model="name">
    -->
    <h2>Reactive demo:</h2>
    <p>{{ninjaTwo.name}} - {{ninjaTwo.age}} - {{nameTwo}}</p>
    <button @click="updateNinjaTwo">Update ninja two</button>


    <!--computed values demo -->
    <input type="text" v-model="search">
    <p>search term - {{search}}</p>
    <div v-for="name in matchingNames" :key="name">{{name}}</div>
  </div>
</template>

<script>
//import { ref } from '@vue/reactivity'
import { ref , reactive, computed} from "vue"

export default {
  name: 'Home',
  setup(){
    
    
    //these are not reactive by default, 
    let nameNotReactive = "mario"
    let ageNotReactive = 30

    //these are reactive
    const name = ref("Rita")
    const age = ref(35)


    //create a reference to the paragraph tag:
      //const p = ref(null)

    const handleClick = () => {
      //p.value.classList.add("testClass")
      //p.value.textContent = "New text from textContent"

      //wont change their values because they are not reactive
      nameNotReactive = "luigi"
      ageNotReactive = 40

      //will change value
      name.value = "Naka"
      age.value = 21
      }

      //with ref
    const ninjaOne = ref({name: "Zoe", age: 13})
    
    const updateNinjaOne = () => {
      ninjaOne.value.age = 1
    }

    //with reactive (does not work on primitive values though)
    const ninjaTwo = reactive({name: "Luigi", age: 60})
    const nameTwo = reactive("Bobi")

    const updateNinjaTwo = () => {
      ninjaTwo.age = 45
      //will not change because nameTwo is a primitive value:
      nameTwo = reactive("Wine")//nope doesnot work
      nameTwo = "Wine" //wont work either
    }
    //============================COMPUTED VALUES=================================
    const search = ref("")
    const namesToSearch = ref(["kate", "Alice", "Rita", "Anna", "Bobi"])
    const matchingNames = computed(() => {
      return namesToSearch.value.filter(() =>name.includes(search.value))
    })

    return {
      //nameinTemplate: valueinSetup
      //name: name, age:age OR
      nameNotReactive, 
      ageNotReactive, 
      handleClick, 
      name, 
      age,
      ninjaOne,
      updateNinjaOne,
      ninjaTwo,
      updateNinjaTwo,
      nameTwo,
      //nameComputed,
      namesToSearch,
      search,
      matchingNames
    }
  }
  
}
</script>
