<!DOCTYPE html>
<html lang="pt-BT">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Extrator de Palavras-Chave</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="container">
        <h1>Extrator de palavras-chave</h1>
        <textarea id="entrada-de-texto" placeholder="Digite ou cole seu texto aqui..."></textarea>
        <button id="botao-palavrachave">Extrair</button>
        <div id="resultado-palavrachave"></div>
    </div>
    <script src="script.js"></script>
</body>

</html>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

:root {
    --cor-destaque: #ED145B;
    --cor-gradiente-preto: linear-gradient(113deg, #000 0%, #1E2021 44.96%, #1E2022 100%);
}

* {
    margin: 0;
    padding: 0;
    font-family: Montserrat;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 16px 21px 18px 21px;
    background: var(--cor-gradiente-preto);
    height: 100vh;
    flex-direction: column;
}


.container {
    display: flex;
    width: 65rem;
    flex-direction: column;
    align-items: center;
    gap: 3rem;
    overflow: hidden;
}

h1 {
    color: var(--cor-destaque);
    text-align: center;
    font-size: 2.8rem;
    font-weight: 600;
    text-transform: uppercase;
}

#entrada-de-texto {
    display: flex;
    height: 12rem;
    padding: 1.4rem 2.5rem 2.5rem 2.5rem;
    align-items: flex-start;
    gap: 0.625rem;
    align-self: stretch;
    border-radius: 0.625rem;
    background: #FFF;
    font-size: 2rem;
}

#entrada-de-texto::placeholder {
    color: #828282;
    font-size: 2rem;
    font-weight: 400;
    line-height: normal;
}

#botao-palavrachave {
    display: flex;
    padding: 1.25rem;
    justify-content: center;
    align-items: center;
    gap: 0.625rem;
    border-radius: 0.5rem;
    border: none;
    background: var(--cor-destaque);
    color: #000;
    font-size: 2.5rem;
    font-weight: 500;
    line-height: normal;
}

#resultado-palavrachave {
    display: flex;
    border-radius: 0.625rem;
    align-self: stretch;
    color: var(--cor-destaque);
    font-size: 2.5rem;
    justify-content: center;
    margin-bottom: 2rem;
    max-width: 100%;
    max-height: 50vh;
    overflow: auto;
}
const botaoMostraPalavras = document.querySelector('#botao-palavrachave');

botaoMostraPalavras.addEventListener('click', mostraPalavrasChave);

function mostraPalavrasChave() {
    const texto = document.querySelector('#entrada-de-texto').value;
    const campoResultado = document.querySelector('#resultado-palavrachave');
    const palavrasChave = processaTexto(texto);

    campoResultado.textContent = palavrasChave.join(", ");
}

function processaTexto(texto) {
    let palavras = texto.split(/\P{L}+/u);
    const frequencias = contaFrequencias(palavras);
    let ordenadas = Object.keys(frequencias).sort(ordenaPalavra);

    function ordenaPalavra(p1, p2) {
        return frequencias[p2] - frequencias[p1];
    }

    console.log(ordenadas);
    return ordenadas.slice(0, 10);
}

function contaFrequencias(palavras) {
    let frequencias = {};
    for (let i of palavras) {
        frequencias[i] = 0;
        for (let j of palavras) {
            if (i == j) {
                frequencias[i]++;
            }
        }
    }
    return frequencias;
}
