<script>
  let days = ["su", "m", "t", "w", "th", "f", "s"];
  let events = [
    {date: 19, eventName: "bday party"},
    {date: 27, eventName: "soccer practice"},
    {date: 31, eventName: "LAN party"},
  ]

  function hasEvent(day) {
    return day == 18 || day == 27;
  }
</script>

<div>
  <!-- calendar -->
  <div class="calendar">
    {#each days as day}
      <div>{day}</div>
    {/each}
    {#each new Array(31).fill(0) as day, i}
      <div>
        {i+1}
        {#if hasEvent(i+1)}
          *
        {/if}
      </div>
    {/each}
  </div>


</div>

<style>
  .calendar {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
  }

  .calendar > div {
    background-color: skyblue;
    margin: 1px;
  }
</style>