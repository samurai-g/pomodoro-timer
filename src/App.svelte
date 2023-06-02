


<script>
/*
TODO
Benachrichtigung vor löschen
To-Do Items cachen
Benutzer Anmeldung
*/

    import Timer from "./Timer.svelte";
    import ToDoList from "./ToDoList.svelte";
    let src = "/logo.png";
</script>

<main>
    <br>
    <img {src} alt="Logo" class="logo" />
    <div>
        <Timer timerDurationMinutes="25" />
        <div class="divider"></div>
        <h3>To-Do List</h3>
        <ToDoList />
    </div>
</main>

<style>
    div {
        text-align: center;
        color: rgb(255, 255, 255);
        padding: 1em;
        max-width: 300px;
        margin: 0 auto;
        border-radius: 12px;
        background: #b4d175;
        background: linear-gradient(28deg, #b4d175 0%, #cfd9ba 100%);
        box-shadow: 10px 10px 5px rgb(233, 233, 233);
    }
    .logo {
        max-width: 200px;
        height: auto;
        display: block;
        margin: 0 auto;
    }
    h3 {
        margin-top: 1.5em;
        margin-bottom: 1em;
    }

    .divider {
        height: .25em;
        margin: 1em 15%;
        padding: 0;
        background: white;
        box-shadow: inset 10px 10px 5px rgb(233, 233, 233) ;
    }

</style>
