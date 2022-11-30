<script lang="ts">
  import { listen } from 'svelte/internal';
import { Table } from 'sveltestrap';
//import { onMount } from 'svelte';
import { Button, Offcanvas } from 'sveltestrap';
  //import { get_binding_group_value, listen, loop_guard } from 'svelte/internal';
  //import BackUpLocalList from './back_up/back_up_localList.svelte';

  // off-canvas toggle
  let open = false;
  let OffcanvasList;
  let selectedIndex;


  //list.name, list.favColor, list.age, list.id
  function toggle(name, favColor, age, id) {
     open = !open;
     OffcanvasList = id;
     selectedIndex = [name, favColor, age, id];
  }

  //let List; //custom list

  // json data
  let List = [
    { name: 'theo', favColor: 'pink', bio: 'bio theo', age: 22, id: 1 },
    { name: 'floriane', favColor: 'blue', bio: 'bio floriane', age: 35, id: 2 },
    { name: 'nico', favColor: 'green', bio: 'bio nico', age: 55, id: 3 },
    { name: 'jéjé', favColor: 'red', bio: 'bio jéjé', age: 35, id: 4 },
    { name: 'Océane', favColor: 'grey', bio: 'bio Océane', age: 15, id: 5 }
  ]

  //$: list_index = JSON.stringify(List);
</script>

<main>
  {#if List === undefined}
    Loading List...
  {:else}   
    <Table dark>
      <thead>
          <tr>
              <th>Name</th>
              <th>Favorite Color</th>
              <th>Age</th>
              <th>Id</th>
          </tr>
      </thead>
      <tbody>
        <!-- ID -->
          {#each List as list}
            <tr>
              <!--Test block -->

              <td>{list.name}</td>
              <td>{list.favColor}</td>
              <td>{list.age}</td>
              <td>{list.id}</td>


              <Button                
                on:click={() => toggle(list.name, list.favColor, list.age, list.id)} 
                >Détails</Button>
            </tr>
          {/each}
      </tbody>
  </Table>
  {/if}


  <!-- OFF Canvas -->
  <div>
    <Offcanvas
      header= Détails
      scroll
      isOpen={open}
      {toggle}
      backdrop={false}
    >

    <!-- content List -->
    {#if List === undefined}
    Loading List...
  {:else}
    <Table dark>
        <thead>
          <tr>
                <th>ligne {OffcanvasList}</th>
            </tr>
        </thead>
        <tbody>
          <th class="_index_left" scope="row"></th>
          <tr>
            {selectedIndex}
          </tr>      
    
        </tbody>
    </Table>
  {/if}
      
  </Offcanvas>
  </div>

</main>

<style>
/*
._index_left {
  color: grey;
  border-style: inset;
  border-radius: 5vh;
  background-color: antiquewhite;

}
._id, ._name, ._type {
  padding-left: 4svh;
  padding-right: 4vh;
  background-color: rgb(119, 108, 108);
  color: white;
}

._id:hover, ._name:hover, ._type:hover {
  color: rgb(198, 198, 214);
  border-color: blue;
  border-style: solid;
  border-width: 0px 0px 1px 0px;
}
*/
</style>