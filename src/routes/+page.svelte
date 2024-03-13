<script lang="ts">
    import { onMount } from "svelte";

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
            homeFillsViewer: true,
            // defaultZoomLevel: 3,
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
        <div id="zoom-out" class="control">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 97.23 106.31">
                <line class="handle" x1="10" y1="96.31" x2="46.97" y2="59.34" />
                <circle
                    class="circle"
                    cx="58.4"
                    cy="38.83"
                    r="38.83"
                    transform="translate(12.31 91.69) rotate(-82.53)"
                />
                <line
                    class="fill"
                    x1="38.35"
                    y1="38.83"
                    x2="76.42"
                    y2="38.83"
                />
            </svg>
        </div>
        <div id="zoom-in" class="control">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 97.09 106.31">
                <line class="handle" x1="10" y1="96.31" x2="46.97" y2="59.34" />
                <circle
                    class="circle"
                    cx="58.26"
                    cy="38.83"
                    r="38.83"
                    transform="translate(10.59 90.12) rotate(-80.78)"
                />
                <line
                    class="fill"
                    x1="39.22"
                    y1="38.83"
                    x2="77.29"
                    y2="38.83"
                />
                <line class="fill" x1="58.26" y1="19.8" x2="58.26" y2="57.87" />
            </svg>
        </div>
        <div id="home" class="control">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 96.72 106.31">
                <line class="handle" x1="10" y1="96.31" x2="46.97" y2="59.34" />
                <circle
                    class="circle"
                    cx="58.26"
                    cy="38.83"
                    r="38.83"
                    transform="translate(10.59 90.12) rotate(-80.78)"
                />
                <circle class="fill" cx="57.89" cy="38.83" r="19.42" />
            </svg>
        </div>
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

    .handle {
        stroke: #ff0000;
        stroke-width: 20px;
        stroke-linecap: round;
    }

    .circle {
        fill: #ff0000;
    }

    .fill {
        fill: none;
        stroke: #fff;
        stroke-width: 13px;
        stroke-linecap: round;
    }

    .control {
        margin-left: 10px;
        display: inline-block;
        cursor: pointer;
        & svg {
            height: 35px;
            &:hover {
                & > .circle {
                    fill: #000000;
                }
                & > .handle {
                    stroke: #000000;
                }
            }
            &:active {
                & > .fill {
                    stroke: #ff0000;
                }
            }
        }
    }

    .osm {
        grid-column: 1 /2;
        grid-row: 1 / 2;
        z-index: 1;
    }
</style>
