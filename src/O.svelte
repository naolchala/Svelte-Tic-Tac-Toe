<style>
    svg {
        height: 70px;
        width: 70px;
    }
    svg circle {
        fill: none;
        stroke: #97f3ff;
        stroke-width: 15px;
        stroke-dasharray: 1000;
        stroke-dashoffset: 0;

        animation: draw 1s linear;
    }

    @keyframes draw {
        from {
            stroke-dashoffset: 1000;
        }
        to {
            stroke-dashoffset: 0;
        }
    }
</style>

<svg viewBox="0 0 100 100">
    <circle cx="50" cy="50" r="40" />
</svg>
