<script lang="ts">
    import {onMount} from 'svelte'

    let date = new Date()

    export let lang:string
    
    function getDayString(day:number, language:string) {
        const dayStringID = [
            'Minggu',
            'Senin',
            'Selasa',
            'Rabu',
            'Kamis',
            'Jumat',
            'Sabtu',
        ]
        const dayStringEN = [
            'Sunday',
            'Monday',
            'Tuesday',
            'Wednesday',
            'Thursday',
            'Friday',
            'Saturday',
        ]
        const dayStringJP = [
            '日曜日',
            '月曜日',
            '火曜日',
            '水曜日',
            '木曜日',
            '金曜日',
            '土曜日',
        ]

        switch (language) {
            case 'en':
                return dayStringEN[day]    

                break;

            case 'id':
                return dayStringID[day]

                break
            
            case 'jp':
                return dayStringJP[day]

                break
        }
    }

    $: day = date.getDay()
    $: hours = date.getHours()
    $: minutes = date.getMinutes()
    $: tanggal = date.getDate()
    $: bulan = date.getMonth()
    $: tahun = date.getFullYear()
    
    onMount(() => {
        const interval = setInterval(() => {
            date = new Date();
        }, 1000)

        return () => {
            clearInterval(interval)
        }
    })

    function addZero(n:number) {
        const getString = n.toString()

        if(getString.length < 2) {
            return '0' + getString
        }else {
            return getString
        }
    }
</script>

<main>
    <div class="time">
        <p class="day">{getDayString(day, lang)}</p>
        {#if lang == 'jp'}
            <p class="date">{tahun}年{bulan}月{tanggal}日</p>
        {:else}
            <p class="date">{tanggal} / {bulan} / {tahun}</p>
        {/if}
        <p class="clock">{addZero(hours)} : {addZero(minutes)}</p>
    </div>
</main>

<style lang="less">
    @font-roboto: 'Roboto Mono', monospace;
    @font-ibm:'IBM Plex Mono', monospace;

    main {
        position: absolute;
        top: 50%;
        left: 15%;
        transform: translate(-50%, -50%);
    }

    .time {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        
        .day {
            font-size: 20px;
            text-transform: uppercase;
            letter-spacing: 14px;
            text-align: left;
            width: 100%;
            font-family: @font-roboto;
            font-weight: 100;
        }

        .date {
            text-align: left;
            width: 100%;
            letter-spacing: 5px;
        }
    
        .clock {
            text-align: left;
            font-size: 64px;
            font-family: @font-ibm;
            font-weight: 100;
        }
    }
</style>