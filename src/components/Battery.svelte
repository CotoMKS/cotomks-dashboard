<script lang="ts">
    import BatteryFull from 'svelte-material-icons/Battery.svelte'
    import Battery90 from 'svelte-material-icons/Battery90.svelte'
    import Battery80 from 'svelte-material-icons/Battery80.svelte'
    import Battery70 from 'svelte-material-icons/Battery70.svelte'
    import Battery60 from 'svelte-material-icons/Battery60.svelte'
    import Battery50 from 'svelte-material-icons/Battery50.svelte'
    import Battery40 from 'svelte-material-icons/Battery40.svelte'
    import Battery30 from 'svelte-material-icons/Battery30.svelte'
    import Battery20 from 'svelte-material-icons/Battery20.svelte'
    import Battery10 from 'svelte-material-icons/Battery10.svelte'
    import BatteryChargingFull from 'svelte-material-icons/BatteryCharging.svelte'
    import BatteryCharging90 from 'svelte-material-icons/BatteryCharging90.svelte'
    import BatteryCharging80 from 'svelte-material-icons/BatteryCharging80.svelte'
    import BatteryCharging70 from 'svelte-material-icons/BatteryCharging70.svelte'
    import BatteryCharging60 from 'svelte-material-icons/BatteryCharging60.svelte'
    import BatteryCharging50 from 'svelte-material-icons/BatteryCharging50.svelte'
    import BatteryCharging40 from 'svelte-material-icons/BatteryCharging40.svelte'
    import BatteryCharging30 from 'svelte-material-icons/BatteryCharging30.svelte'
    import BatteryCharging20 from 'svelte-material-icons/BatteryCharging20.svelte'
    import BatteryCharging10 from 'svelte-material-icons/BatteryCharging10.svelte'
    
    let chargingStatus = false;
    let batteryLevel

    (navigator as any).getBattery().then(b => {
        chargingStatus = b.charging
        batteryLevel = b.level * 100
        batteryLevel = batteryLevel.toFixed()

        b.addEventListener('chargingchange', () => {
            chargingStatus = b.charging 
        })

        b.addEventListener('levelchange', () => {
            batteryLevel = b.level * 100
            batteryLevel = batteryLevel.toFixed()
        })
    })
</script>

<main>
    {#if chargingStatus}
        {#if batteryLevel > 90}
            <BatteryChargingFull width='24' height='24' />
        {:else if batteryLevel > 80}
            <BatteryCharging90 width='24' height='24' />
        {:else if batteryLevel > 70}
            <BatteryCharging80 width='24' height='24' />
        {:else if batteryLevel > 60}
            <BatteryCharging70 width='24' height='24' />
        {:else if batteryLevel > 50}
            <BatteryCharging60 width='24' height='24' />
        {:else if batteryLevel > 40}
            <BatteryCharging50 width='24' height='24' />
        {:else if batteryLevel > 30}
            <BatteryCharging40 width='24' height='24' />
        {:else if batteryLevel > 20}
            <BatteryCharging30 width='24' height='24' />
        {:else if batteryLevel > 10}
            <BatteryCharging20 width='24' height='24' />
        {:else}
            <BatteryCharging10 width='24' height='24' />
        {/if}
    {:else}
        {#if batteryLevel > 90}
            <BatteryFull width='24' height='24' />
        {:else if batteryLevel > 80}
            <Battery90 width='24' height='24' />
        {:else if batteryLevel > 70}
            <Battery80 width='24' height='24' />
        {:else if batteryLevel > 60}
            <Battery70 width='24' height='24' />
        {:else if batteryLevel > 50}
            <Battery60 width='24' height='24' />
        {:else if batteryLevel > 40}
            <Battery50 width='24' height='24' />
        {:else if batteryLevel > 30}
            <Battery40 width='24' height='24' />
        {:else if batteryLevel > 20}
            <Battery30 width='24' height='24' />
        {:else if batteryLevel > 10}
            <Battery20 width='24' height='24' />
        {:else}
            <Battery10 width='24' height='24' />
        {/if}
    {/if}

    {batteryLevel}%
</main>

<style scoped lang="less">
    main {
        position: absolute;
        left: 10%;
        top: 65%;
        transform: translate(-50%, -50%);
        opacity: 0.3;
        display: flex;
        align-items: center;
        gap: 10px;
    }
</style>