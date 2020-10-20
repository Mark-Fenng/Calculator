<script lang="ts">
    let result: number = 0;
    let formula: string = "",
        formulaText: string = "";
    let digit: string = "";
    $: dotFlag = digit.indexOf(".") !== -1;
    $: symbolFlag = Number.isNaN(Number.parseInt(formula[formula.length - 1]));

    function clickHandler(event: MouseEvent): void {
        if (event.target instanceof HTMLElement) {
            let buttonText = event.target.innerText;
            switch (buttonText) {
                case "c":
                    formula = "";
                    formulaText = "";
                    digit = "";
                    result = 0;
                    dotFlag = false;
                    break;
                case "<":
                    if (formula.length > 0) {
                        formula = formula.slice(0, -1);
                        while (formulaText[formulaText.length - 1] === " ") formulaText = formulaText.slice(0, -1);
                        formulaText = formulaText.slice(0, -1);
                    }
                    break;
                case "÷":
                    digit = "";
                    formula += "/";
                    formulaText += buttonText;
                    break;
                case "x":
                    digit = "";
                    formula += "*";
                    formulaText = `${formulaText}  ${buttonText} `;
                    break;
                case "-":
                case "+":
                    digit = "";
                    formula += buttonText;
                    formulaText += buttonText;
                    break;
                case "=":
                    formula = result.toString();
                    formulaText = formula;
                    digit = formula;
                    break;
                case "%":
                    break;
                case "":
                    break;
                default:
                    digit += buttonText;
                    formula += buttonText;
                    formulaText += buttonText;
                    result = eval(formula);
            }
        }
    }
</script>

<style>
    .Calculator {
        max-width: 21.5em;
    }
    h1 {
        height: 1em;
        text-align: right;
    }
    .Buttons {
        display: grid;
        grid-template-columns: repeat(4, 5em);
        grid-template-rows: repeat(5, 3em);
        grid-gap: 0.5em;
    }

    button {
        margin: 0;
    }
</style>

<div class="Calculator">
    <h1 style="color: #333;">{formulaText}</h1>
    <h1 style="color: #333">{result}</h1>
    <div class="Buttons" on:click={clickHandler}>
        <button>c</button>
        <button>&lt;</button>
        <button>%</button>
        <button disabled={symbolFlag}>÷</button>
        <button>7</button>
        <button>8</button>
        <button>9</button>
        <button disabled={symbolFlag}>x</button>
        <button>4</button>
        <button>5</button>
        <button>6</button>
        <button disabled={symbolFlag}>-</button>
        <button>1</button>
        <button>2</button>
        <button>3</button>
        <button disabled={symbolFlag}>+</button>
        <button />
        <button disabled={formula[formula.length - 1] === '/'}>0</button>
        <button disabled={dotFlag}>.</button>
        <button>=</button>
    </div>
</div>
