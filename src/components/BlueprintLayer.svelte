<script>
    import { Rect } from 'svelte-konva';

    export let cellCountWidth;
    export let cellCountHeight;
    export let gridSize;

    let wallsState = [];

    function generateWallsBlueprint() {
        const blueprint = [];
        const wallDepth = 15;

        for (let i = 0; i < cellCountWidth; i++) {
            for (let j = 0; j < cellCountHeight; j++) {
                const wallId = i * cellCountHeight + j;

                blueprint.push({
                    x: i * gridSize - wallDepth / 2 + 1,
                    y: j * gridSize - wallDepth / 2 + 1,
                    width: wallDepth,
                    height: gridSize + wallDepth,
                    fill: 'transparent',
                    stroke: wallsState[wallId] === 'pressed' ? 'blue' : wallsState[wallId] === 'hovered' ? 'lightblue' : '#000',
                    strokeWidth: 1,
                    dash: [2, 2],
                    wallId,
                });

                blueprint.push({
                    x: i * gridSize - wallDepth / 2 + 1,
                    y: j * gridSize - wallDepth / 2 + 1,
                    width: gridSize + wallDepth,
                    height: wallDepth,
                    fill: 'transparent',
                    stroke: wallsState[wallId] === 'pressed' ? 'blue' : wallsState[wallId] === 'hovered' ? 'lightblue' : '#000',
                    strokeWidth: 1,
                    dash: [2, 2],
                    wallId,
                });
            }
        }

        // Генерация последней порции стен для правого края и нижнего
        for (let i = 0; i < cellCountHeight; i++) {
            const wallId = cellCountWidth * cellCountHeight + i;

            blueprint.push({
                x: cellCountWidth * gridSize - wallDepth / 2 + 1,
                y: i * gridSize - wallDepth / 2 + 1,
                width: wallDepth,
                height: gridSize + wallDepth,
                fill: 'transparent',
                stroke: wallsState[wallId] === 'pressed' ? 'blue' : wallsState[wallId] === 'hovered' ? 'lightblue' : '#000',
                strokeWidth: 1,
                dash: [2, 2],
                wallId,
            });
        }

        for (let i = 0; i < cellCountWidth; i++) {
            const wallId = (cellCountWidth + 1) * cellCountHeight + i;

            blueprint.push({
                x: i * gridSize - wallDepth / 2 + 1,
                y: cellCountHeight * gridSize - wallDepth / 2 + 1,
                width: gridSize + wallDepth,
                height: wallDepth,
                fill: 'transparent',
                stroke: wallsState[wallId] === 'pressed' ? 'blue' : wallsState[wallId] === 'hovered' ? 'lightblue' : '#000',
                strokeWidth: 1,
                dash: [2, 2],
                wallId,
            });
        }

        return blueprint;
    }

    function handleWallMouseEnter(event) {
        event.detail.target.attrs.fill = '#f00';
    }

    function handleWallMouseLeave(event) {
        // const wallId = event.target.attrs.wallId;
        // wallsState[wallId] = '';
        // console.log('bop');
    }

    function handleWallClick(event) {
        // const wallId = event.target.attrs.wallId;
        // wallsState[wallId] = wallsState[wallId] === 'pressed' ? '' : 'pressed';
    }
</script>

{#each generateWallsBlueprint() as { x, y, width, height, fill, stroke, strokeWidth, dash, wallId }, i}
    <Rect
            config={{
            x: x,
            y: y,
            width: width,
            height: height,
            fill: fill,
            stroke: stroke,
            strokeWidth: strokeWidth,
            dash: dash,
        }}
            on:mouseenter={handleWallMouseEnter}
            on:mouseleave={handleWallMouseLeave}
            on:click={handleWallClick}
    />
{/each}
