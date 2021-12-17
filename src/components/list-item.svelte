<script>
 import { createEventDispatcher } from 'svelte';
 const dispatch = createEventDispatcher();
 import Text from "../elements/item-text.svelte";
 export let selected
 export let userName
 export let userSurname
 export let throughtName
 export let throughtSurname
 export let clickOnAdd
 
</script>

<div on:click = {()=> dispatch('clickOnName')}>
  <Text
    {selected}
    mainText = {userName}
    throughtText = {throughtName}
    {clickOnAdd}
  />
  <Text
   {clickOnAdd}
   {selected}
   mainText = {userSurname}
   throughtText = {throughtSurname}
  />
  <button on:click|stopPropagation>Удалить</button>
</div>   


<style>
  button{
    color: #FF2424;
    background: transparent;
    border: none;
    cursor: pointer;
    font-size: 10px;
    line-height: 12px;
    margin-top: 4px;
  }

  button:hover{
   background: rgba(255, 57, 57, 0.3);
  }

  div{
   height: 25px;
   margin: 5px 20px;
   display: flex;
   justify-content: space-between;
   align-items: center;
   font-size: 12px;
   line-height: 14px;
   margin: 5px 20px;
   background: #D5D5D5;
   box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.25);
   border-radius: 5px;
   padding-left: 10px;
   padding-right: 10px;
   cursor: pointer;
   border: 1px solid #D5D5D5;
  } 

  div:hover{
   border: 1px solid #404040;
   box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.25);
  }
</style>