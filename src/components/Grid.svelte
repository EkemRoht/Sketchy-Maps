<script>
    import { Stage, Layer, Line, Rect } from 'svelte-konva';
    import { onMount } from 'svelte';

    let width = window.innerWidth;
    let height = window.innerHeight;
    let gridSize = 50;
    let gridWidth = 10;
    let gridHeight = 10;
    let lines = generateGrid();

    function generateGrid() {
        const lines = [];
        const dashLength = 1; // Расчет длины штрихов

        for (let i = 0; i <= gridWidth * gridSize; i += gridSize) {
            lines.push({
                points: [i + 0.5, 0, i + 0.5, height],
                strokeWidth: 1,
                dash: [dashLength, dashLength*3],
            });
        }

        for (let j = 0; j <= gridHeight * gridSize; j += gridSize) {
            lines.push({
                points: [0, j + 0.5, width, j + 0.5],
                strokeWidth: 1,
                dash: [dashLength, dashLength*3],
            });
        }

        return lines;
    }

    function generateCrosses() {
        const crosses = [];

        for (let i = 0; i < width; i += gridSize) {
            for (let j = 0; j < height; j += gridSize) {
                crosses.push({
                    x: i + 0.5,
                    y: j + 0.5,
                });
            }
        }

        return crosses;
    }
</script>

<Stage config={{ width, height, draggable: true }}>
    <Layer>
        <!-- Отрисовываем линии сетки -->
        {#each lines as { points, stroke, strokeWidth, dash }, i}
            <Line
                    config={{
                    points: points,
                    stroke: '#aaa',
                    strokeWidth: strokeWidth,
                    dash: dash,
                }}
            />
        {/each}
        <!-- Отрисовываем крестики на пересечениях линий сетки -->
        {#each generateCrosses() as { x, y }, i}
            <Line
                    config={{
                    points: [x - 3, y, x + 3, y],
                    stroke: '#666',
                    strokeWidth: 1,
                }}
            />
            <Line
                    config={{
                    points: [x, y - 3, x, y + 3],
                    stroke: '#666',
                    strokeWidth: 1,
                }}
            />
        {/each}
    </Layer>
</Stage>
