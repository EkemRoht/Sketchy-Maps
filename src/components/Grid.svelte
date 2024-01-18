<script>
    import { Stage, Layer, Line } from 'svelte-konva';

    let width = window.innerWidth;
    let height = window.innerHeight;
    let gridSize = 50;

    function generateGrid() {
        const lines = [];

        for (let i = 0; i <= width; i += gridSize) {
            lines.push({
                points: [i + 0.5, 0, i + 0.5, height],
                stroke: 'gray',
                strokeWidth: 1
            });
        }

        for (let j = 0; j <= height; j += gridSize) {
            lines.push({
                points: [0, j + 0.5, width, j + 0.5],
                stroke: 'gray',
                strokeWidth: 1
            });
        }

        return lines;
    }
</script>

<Stage config={{ width, height }}>
    <Layer>
        {#each generateGrid() as { points, stroke, strokeWidth }, i}
            <Line
                    config={{
                    points: points,
                    stroke: stroke,
                    strokeWidth: strokeWidth
                }}
            />
        {/each}
    </Layer>
</Stage>
