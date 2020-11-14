<script>

    import { logout } from "../firebaseBackend"
    import { userDataStore } from "../stores/userDataStore"
</script>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>

    <h1>Svelte Firebase Starter</h1>
    <!--
    {@debug $userDataStore}
-->
    {#if $userDataStore}
        {#if !$userDataStore.displayName && !$userDataStore.email}
            <p>Please complete your profile in Settings</p>
        {:else}
            <p>Logged in as {$userDataStore.displayName || $userDataStore.email}</p>
        {/if}
    {:else}
        <p>Not logged in</p>
    {/if}
    <div>
        <a href="/" >Home</a>
        {#if !$userDataStore}
            <a href="/register" >Register</a>
            <a href="/signin" >Signin</a>
        {:else}
            <a href="{$userDataStore.username}" >Profile</a>

            <a href="/settings" >Settings</a>
            <button on:click="{logout}">Logout</button>
        {/if}
        <a href="/users" >Users</a>

        <hr />

        <div>

            <slot />
        </div>
    </div>
