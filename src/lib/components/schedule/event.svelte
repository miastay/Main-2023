<script lang="ts">
	import type { SvelteComponent } from 'svelte';
	import type { ComponentType } from 'svelte/internal';
    import Event from './event.svelte';
    import EventModal from './event_modal.svelte';
    import { writable, type Writable } from "svelte/store";

    import './schedule.scss';

	export let title: string;
    export let description: string;
	export let hour_start: number;
    export let minute_start: number;
	export let length_minutes: number;
    export let display_width: number;
    export let display_column: number;
    export let color: string;
    export let eventIsHovered: boolean;
	export let alt: string;
    export let this_component: ComponentType;

    let state_title = title;
    let isModalOpen = false;

    function toggleModal () {
        isModalOpen = !isModalOpen;
        console.log(isModalOpen)
    }

</script>

<div on:click={() => toggleModal()} on:mouseover={() => {eventIsHovered = true;}} on:mouseout={() => {eventIsHovered = false;}} class='event h{((hour_start * 6) + (Math.floor(minute_start / 10)))} {color} w{display_width} l{Math.ceil(length_minutes / 10)} c{display_column} {eventIsHovered ? ' hovered' : ''}'>
    {title}
    
</div>
{#if isModalOpen}
        <div on:click={() => toggleModal()}>
            <EventModal 
                            title={title}
                            description={description}
                            hour_start={hour_start}
                            minute_start={minute_start}
                            length_minutes={length_minutes}
                        />
        </div>
{/if}


<!-- <div on:click={() => openModal(event)} on:mouseover={() => {eventIsHovered = true;}} on:mouseout={() => {eventIsHovered = false;}} class='event h{((event.hour_start * 6) + (Math.floor(event.minute_start / 10)))} {event.color} w{event.display_width} l{Math.ceil(event.length_minutes / 10)} c{event.display_column} {eventIsHovered ? ' hovered' : ''}'>
                    {event.title}
                     <span class='inner'> &nbsp;({event.length_minutes})</span> 
                </div> -->
