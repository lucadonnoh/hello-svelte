<script>
    let funnyPeople = [
        { name: "Juri Fabbri" },
        { name: "Geronimo Stilton anti-israelita" },
        { name: "Bob Marley" }
    ]
</script>

<p>other funny people as you: </p>
<ul style="list-style-type: none">
    {#each funnyPeople as person, i}
    <li>
        {i + 1}: {person.name}
    </li>
    {/each}
</ul>