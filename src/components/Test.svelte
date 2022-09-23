<script>

  let addPropery = false;
  let noProperty = true;
 
import { object_without_properties } from "svelte/internal";

 let id, type, number, street, owner, boughtFor, soldFor;

  let account = {};
  let property = {};

  function addProperty() {

    account.property.push(
      type = type,
      number = number,
      street = street,
      owner = owner,
      boughtFor = boughtFor,
      soldFor = soldFor,
    );
    noProperty = false;
    addProperty = true;
  }

</script>

<div>
  {#if noProperty}
    <form>
      <input type="text" bind:value={type} placeholder="type">
      <input type="number" bind:value={number} placeholder="number">
      <input type="text" bind:value={street} placeholder="street">
      <input type="text" bind:value={owner} placeholder="owner">
      <input type="number" bind:value={boughtFor} placeholder="bought for">
      <input type="number" bind:value={soldFor} placeholder="sold for">
      <button on:click={addProperty}>add property</button>
    </form>
  {/if}
  {#if addProperty}
    <div>
      <ul>
        <p>Your properties:</p>

          <li>{property.type}</li>
          <li>{property.boughtFor}</li>

      </ul>
    </div>
  {/if}
</div>

<style>

</style>