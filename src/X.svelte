<style>
    svg {
        height: 70px;
        width: 70px;
    }
    svg line {
        stroke: #97f3ff;
        stroke-width: 15px;
        stroke-dasharray: 1000;
        stroke-dashoffset: 0;

        animation: draw 2s linear;
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
    <line x1="0" y1="0" x2="100" y2="100" />
    <line x1="100" y1="0" x2="0" y2="100" />
</svg>
