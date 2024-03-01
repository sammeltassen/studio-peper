<script lang="ts">
    import { onMount } from "svelte";
    import { zoomIn, zoomOut, home } from "$lib/svg";

    let container: HTMLElement;
    // let zoomIn: HTMLElement;
    // let zoomOut: HTMLElement;
    // let home: HTMLElement;

    onMount(async () => {
        const openSeaDragon = await import("openseadragon");
        const options = {
            // constrainDuringPan: true,
            // preserveViewport: true,
            element: container,
            homeButton: "home",
            zoomInButton: "zoom-in",
            zoomOutButton: "zoom-out",
            // minZoomLevel: 0,
            prefixUrl: "https://openseadragon.github.io/openseadragon/images/",
            showNavigator: false,
            gestureSettingsMouse: { clickToZoom: false },
            tileSources: [
                {
                    //required
                    type: "zoomifytileservice",
                    width: 21000,
                    height: 11811,
                    tilesUrl: "/tiles/",
                    //optional
                    tileSize: 256,
                    fileFormat: "jpg",
                },
            ],
            // tileSources: initialTileSources,
            // visibilityRatio: 1
        };

        const viewer = new openSeaDragon.Viewer(options);
    });
</script>

<div class="grid">
    <div class="osm" bind:this={container}></div>
    <div class="control-container">
        <div id="zoom-out" class="control">{@html zoomOut}</div>
        <div id="zoom-in" class="control">{@html zoomIn}</div>
        <div id="home" class="control">{@html home}</div>
    </div>
</div>

<style>
    :global(html, body) {
        font-family:
            Helvetica Neue,
            Helvetica,
            Arial,
            sans-serif;
        font-size: 15px;
        padding: 0;
        margin: 0;
        overflow: hidden;
    }

    .grid {
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr;
        width: 100vw;
        height: 100vh;
        background-color: white;
    }

    .control-container {
        grid-column: 1 /2;
        grid-row: 1 / 2;
        z-index: 2;
        pointer-events: none;
        margin-top: 15px;
    }

    .control {
        margin-left: 10px;
        & svg {
            height: 35px;
        }
    }

    .osm {
        grid-column: 1 /2;
        grid-row: 1 / 2;
        z-index: 1;
    }
</style>
