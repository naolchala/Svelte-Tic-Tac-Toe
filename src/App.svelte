<script>
    import X from "./X.svelte";
    import O from "./O.svelte";

    let game = [...new Array(9)];
    game.forEach((item, index) => {
        game[index] = 0;
    });

    let turn = 1;
    let finished = false;
    let draw = false;

    const changeCell = (index) => {
        if (game[index] === 0) {
            game[index] = turn;
            checkwin();
            if (!finished) {
                if (!checkDraw()) {
                    changePlayer();
                } else {
                    draw = true;
                }
            }
        }
    };

    const checkwin = () => {
        const winingData = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6],
        ];

        winingData.forEach((item, index) => {
            if (
                game[item[0]] !== 0 &&
                game[item[1]] !== 0 &&
                game[item[2]] !== 0
            ) {
                if (
                    game[item[0]] === game[item[1]] &&
                    game[item[1]] === game[item[2]]
                ) {
                    finished = true;
                }
            }
        });
    };

    const checkDraw = () => {
        let d = true;
        if (!finished) {
            game.forEach((item) => {
                if (item === 0) {
                    d = false;
                }
            });
        }

        return d;
    };

    const changePlayer = () => (turn === 1 ? (turn = 2) : (turn = 1));

    const restart = () => {
        game.forEach((item, index) => {
            game[index] = 0;
        });
        finished = false;
        draw = false;
    };
</script>

<style>
    main {
        width: 100%;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .board {
        background: rgba(255, 255, 255, 0.2);
        border-top: 1px solid #fff5;
        border-left: 1px solid #fff5;
        border-radius: 6px;

        box-shadow: 0 0 50px 20px #000a;

        backdrop-filter: blur(5px);
        display: grid;
        grid-template-columns: 150px 150px 150px;
    }

    .cell {
        display: flex;
        align-items: center;
        justify-content: center;

        font-size: 3em;
        height: 150px;
        transition: all 1s ease;
    }
    .board .cell:nth-child(3n + 2) {
        border-left: 1px solid #fff5;
        border-right: 1px inset #fff5;
    }
    .board .cell:nth-child(4),
    .board .cell:nth-child(5),
    .board .cell:nth-child(6) {
        border-top: 1px solid #fff5;
        border-bottom: 1px inset #fff5;
    }

    .cell:hover {
        background: #fff4;
        transition: all 0.2s;
    }
    .photo-owner {
        position: fixed;
        bottom: 30px;
        color: white;
        font-size: small;
    }
    .modal {
        position: fixed;
        z-index: 1000;
    }
    .modal::after {
        content: "";
        display: block;
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;

        backdrop-filter: blur(10px);
        z-index: 100;
    }
    .modal .content {
        background: rgba(255, 255, 255, 0.2);
        border-top: 1px solid #fff5;
        border-left: 1px solid #fff5;
        border-radius: 6px;
        box-shadow: 0 0 50px 20px #0003;
        backdrop-filter: blur(5px);
        text-align: center;
        padding: 15px;
        color: white;
        z-index: 200;
        width: clamp(200px, 15vw, 50%);
        animation: modalApper 200ms ease-in;
    }

    .modal .content button {
        background: #00bcd4;
        border: none;
        outline: none;
        color: white;
        border-radius: 5px;
        width: 100%;
    }

    @keyframes modalApper {
        from {
            transform: scale(0.5);
        }
        to {
            transform: scale(1);
        }
    }
</style>

<main>
    {#if finished}
        <main class="modal">
            <div class="content">
                <h1>Player {turn === 1 ? 'X' : 'O'} won</h1>
                <button on:click={restart}>Restart Game</button>
            </div>
        </main>
    {:else if draw}
        <main class="modal">
            <div class="content">
                <h1>its Draw</h1>
                <button on:click={restart}>Restart Game</button>
            </div>
        </main>
    {/if}

    <div class="board">
        {#each game as cell, index}
            <div class="cell" on:click={() => changeCell(index)}>
                {#if cell === 1}
                    <X />
                {:else if cell === 2}
                    <O />
                {/if}
            </div>
        {/each}
    </div>
    <span class="photo-owner"><span>Photo by
            <a
                href="https://unsplash.com/@keithmisner?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Keith
                Misner</a>
            on
            <a
                href="https://unsplash.com/s/photos/background?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span></span>
</main>
