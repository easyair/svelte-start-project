<script>
 import Btn from './elements/btn.svelte'
 import Item from './components/list-item.svelte'
 import CardToEdit from './components/cardToEdit.svelte'
 import CardToAdd from './components/cardToAdd.svelte'
 
 let selected = null
 let clickOnAdd = false
 let throughtName
 let throughtSurname
 let key
 let addNewUserName ="Новое имя"
 let addNewUserSurname = "Новая фамилия"
 let cancelEditButton = "Закрыть"
 let disableSaveEditButton


 let users = [
   {  id:1, firstName: "Иван", secondName: "Иванов" },
   {  id:2 ,firstName: "Петр", secondName: "Петров" },
   {  id:3 ,firstName: "Михаил", secondName: "Михаилов" },
   {  id:4 ,firstName: "Василий", secondName: "Васильев" }
 ]

 let idx = users.length +1
 users = users.sort(SortArray)

 function SortArray(x, y){
   if (x.firstName < y.firstName) {return -1;}
   if (x.firstName > y.firstName) {return 1;}
   return 0;
 }


 function openEditCard(user,index){
   selected = {
     user,
     a:{
       firstName: user.firstName,
       secondName: user.secondName
     }
   }
  
   clickOnAdd=true
   throughtName = selected.a.firstName
   throughtSurname = selected.a.secondName
   console.log((selected.user.id == user.id) ? selected:null)
   key=index
 }

 function saveEdit(){
    clickOnAdd=false
    selected = null
    users = users.sort(SortArray)
    cancelEditButton = "Закрыть"
    disableSaveEditButton = true
 }
 
 function cancelEdit(){
   clickOnAdd=false
   selected=null
   users[key].firstName=throughtName
   users[key].secondName=throughtSurname
   cancelEditButton = "Закрыть"
   disableSaveEditButton = true
 }

 function deleteItem(user){
   if(!selected){
    users = users.filter((item)=> item != user)
   }
    
 }

 function cancelAddNewUser(){
    clickOnAdd=false
    addNewUserName ="Новое имя"
    addNewUserSurname = "Новая фамилия"
 }

 function addNewUser(){
    users = users.concat([{
      id:idx,
      firstName: addNewUserName,
      secondName: addNewUserSurname
    }])
    .sort(SortArray)
    
    clickOnAdd=false
    addNewUserName ="Новое имя"
    addNewUserSurname = "Новая фамилия"
    idx++
 }

 function changeEditCardButton(){
   if(throughtName != users[key].firstName || throughtSurname != users[key].secondName){
     cancelEditButton ="Отменить изменения"
     disableSaveEditButton = false
   }else{
    cancelEditButton = "Закрыть"
    disableSaveEditButton = true
   }
 }

</script>


<main>
	<div class="main-container">
		<div class="header-block">
      <Btn
       on:click = {()=> clickOnAdd=true}
       btnText="Добавить нового пользователя"
       clickable={clickOnAdd}
      />
		</div>
		<div class="list-block">
      {#if clickOnAdd && !selected}
        <Item
         userName={addNewUserName}
         userSurname={addNewUserSurname}
         {clickOnAdd}
        />
      {/if}
      {#each users as user,index}
       <Item
        on:clickOnName={openEditCard(user,index)}
        on:click = {deleteItem(user)}
        userName={user.firstName}
        userSurname= {user.secondName}
        {throughtName}
        {throughtSurname}
        selected = {(selected?.user.id == user.id)?selected:null}
       />
      {/each}
		</div>
	</div>
  {#if clickOnAdd && !selected}
    <CardToAdd
     bind:cardName={addNewUserName}
     bind:cardSurname={addNewUserSurname}
     on:clickedAgree = {addNewUser}
     on:clickedCancel={cancelAddNewUser}
    />
  {/if}
  {#if selected}
    <CardToEdit
     bind:cardName={users[key].firstName}
     bind:cardSurname = {users[key].secondName}
     on:clickedAgree={saveEdit}
     on:clickedCancel={cancelEdit}
     on:input={changeEditCardButton}
     {cancelEditButton}
     {disableSaveEditButton}
    />
  {/if}
</main>


<style>

  .main-container{
    background-color: #999999;
    height: 100%;
    min-width: 600px;
    width: 40%;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 5px
  } 
  .header-block{
    padding: 10px ;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-end;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    margin-bottom: 20px;
  } 
  main {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
  }

</style>