<script lang="ts">
    import { onMount } from "svelte";
    import { browser } from '$app/environment';
    import { goto } from '$app/navigation';
    
    export let passcondition:boolean;
    export let logout:boolean=true;
    export let redirect:string="/settings/profile";
    
    onMount(async () => { if(browser && !passcondition) {
        if(logout) {
            // Cleanup what ever stores and databases you must
            goto("/");
        }
        else goto(redirect);        
    }});
    </script>
    
    {#if passcondition} <slot /> {/if}