<script>
    import { Line } from 'svelte-konva';

    export let gridSize;
    export let cellCountWidth;
    export let cellCountHeight ;
    let lines = generateGrid();

    function generateGrid() {
        const lines = [];
        const dashLength = 1; // Расчет длины штрихов

        for (let i = 0; i <= cellCountWidth; i++) {
            lines.push({
                points: [i * gridSize + 0.5, 0, i * gridSize + 0.5, cellCountHeight * gridSize],
                strokeWidth: 1,
                dash: [dashLength, dashLength * 3],
            });
        }

        for (let j = 0; j <= cellCountHeight; j++) {
            lines.push({
                points: [0, j * gridSize + 0.5, cellCountWidth * gridSize, j * gridSize + 0.5],
                strokeWidth: 1,
                dash: [dashLength, dashLength * 3],
            });
        }

        return lines;
    }

    function generateCrosses() {
        const crosses = [];

        for (let i = 0; i <= cellCountWidth; i++) {
            for (let j = 0; j <= cellCountHeight; j++) {
                crosses.push({
                    x: i * gridSize + 0.5,
                    y: j * gridSize + 0.5,
                });
            }
        }

        return crosses;
    }
</script>

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