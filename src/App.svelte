<script>
    import { Stage, Layer } from 'svelte-konva';
    import Grid from "./components/Grid.svelte";
    import BlueprintLayer from "./components/BlueprintLayer.svelte";

    let width = window.innerWidth;
    let height = window.innerHeight;
    let gridSize = 50;
    let cellCountWidth = 10;
    let cellCountHeight = 10;
</script>

<Stage config={{ width, height, draggable: true }}>
    <Layer>
        <BlueprintLayer {cellCountWidth} {cellCountHeight} {gridSize} />
        <Grid {cellCountWidth} {cellCountHeight} {gridSize} />
    </Layer>
</Stage>