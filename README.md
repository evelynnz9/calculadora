<!DOCTYPE html>
    <html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Pagina Inicial</title>
    <style>
        /* Reset básico */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
}

/* Estilo do corpo */
body {
    background: linear-gradient(135deg, #3d7dcbff, #165a6fff);
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

/* Container da calculadora */
form {
    background: #2c3e50;
    padding: 20px 30px;
    border-radius: 12px;
    box-shadow: 0px 8px 18px rgba(0, 0, 0, 0.3);
    text-align: center;
}

/* Título */
h1 {
    text-align: center;
    margin-bottom: 20px;
    color: #ecf0f1;
}

/* Labels */
label {
    font-weight: bold;
    display: block;
    margin-bottom: 8px;
    color: #ecf0f1;
}

/* Inputs */
input[type="number"], input[type="text"] {
    width: 100%;
    padding: 10px;
    border-radius: 6px;
    border: none;
    margin-bottom: 15px;
    outline: none;
    font-size: 16px;
}

/* Botões */
button {
    background: #27ae60;
    color: white;
    border: none;
    padding: 10px 18px;
    margin: 6px;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #1e8449;
    transform: scale(1.05);
}

/* Resultado */
h4 {
    margin-top: 20px;
    text-align: center;
}

#resultado {
    margin-top: 10px;
    padding: 12px;
    background: #34495e;
    border-radius: 8px;
    text-align: center;
    font-weight: bold;
    font-size: 18px;
    color: #f1c40f;
}
    </style>
</head>
<body>
   <form>
        <h2>Calculadora básica</h2><br>
        <!-- LABEL é a parte Que descreve uma caixa -->
        <label for="num1">Informe o 1° número</label>
        <!-- INPUT é uma area que pode ser alterada pelo usuario -->
        <input id="num1" type="number"> 
        <!-- BR pula linhas -->
        <br><br>
        <label for="num2">Informe o 2° número</label>
        <input id="num2" type="number">
        <br><br>
        <!-- Adiciona botoes na tela que quando sao clicados(onclick) chamam uma função -->
        <button type="button" onclick="calcular('somar')">Somar</button>
        <button type="button" onclick="calcular('subtrair')">Subtrair</button>
        <button type="button" onclick="calcular('multiplicar')">Multiplicar</button>
        <button type="button" onclick="calcular('dividir')">Dividir</button>
        <br><br>
        <hr><br>
        <label for="Pokemon">informe um pokemon</label>
        <input id="pokemon" type="text" placeholder="Ex: Pikachu">
            <button type="button" onclick="insiraPokemon()">Inserir Pockemon</button>
            <h4>Resultado:</h4>
            <div id="resultado"></div>
            <div id="pokemon-info"></div>
    </form>
    
    <script>
        
   
        // função em javascript
        function calcular(operacao){
            // var declarava uma variavel
            // parseFloat converte o conteudo para numero decimal
            // document.getElementById pega o elemento do HTML pelo ID
            var num1 = parseFloat(document.getElementById('num1').value);
            var num2 = parseFloat(document.getElementById('num2').value);

            // escolha caso em javascript:
            switch(operacao){
                case 'somar':
                    var resultado = num1 + num2;
                    break;
                case 'subtrair':
                    var resultado = num1 - num2;
                    break;
                case 'multiplicar':
                    var resultado = num1 * num2;
                    break;
                case 'dividir':
                    // se em javascript
                    if(num2 == 0){
                        var resultado = "Não é possível dividir por zero";
                    }else{
                        var resultado = num1 / num2;
                    }
                    break;
                default:
                    var resultado = 0;
     
            }

            document.getElementById("resultado").textContent = resultado;
            
        var pokemon = resultado
        fetch("https://pokeapi.co/api/v2/pokemon/" + pokemon)
        .then(res => res.json())
        .then(data => {
            console.log(data)
            document.getElementById("pokemon-info").innerHTML = '<p>Nome: '+ data.name + ', Altura:' + data.height + ', peso: ' + data.weight + '</p>';
                document.getElementById("pokemon-info").innerHTML += '<br><img src="'+data.sprites.front_default +'" width="150">';
              
            })
    .catch(error => {
     
        fetch("https://api.thecatapi.com/v1/images/search")
       .then(res => res.json())
       .then(data => {
        console.log(data)
            document.getElementById("resultado").innerHTML += "<br><img src='"+data[0].url+"' width = '300px'>";
        })});
       };
         

//             // mostrando o resultado no console do navegador (F12)
//             console.log(resultado);
//             // pegando o elemento pelo ID e falando q o texto contido é = resultado
//             document.getElementById('resultado').textContent = resultado;
//         }
//     // Exemplo de requisição para um API pública
//     // fech + link do API é usado para fazer requisições HTTP
//     fetch("https://api.thecatapi.com/v1/images/search")
//         // A resposta é convertida para JSON
//         .then(res => res.json())
//         // os dados são armazenados na variável data
//         .then(data => {
//         // Armazena os valores no CONSOLE
//             console.log(data)
//             // Adiciona a imagem do gato na página
//             document.getElementById("resultado").innerHTML += "<br><img src='"+data[0].url+"' width = '300px'>";
//         })
//  // fech + link do API é usado para fazer requisições HTTP
// fetch("https://pokeapi.co/api/v2/pokemon/pikachu")
//         // A resposta é convertida para JSON
//         .then(res => res.json())
//         // Os dados são armazenados na variável data
//         .then(data => {
//             console.log(data)
//             // Adiciona a imagem do gato na página
//             document.getElementById("resultado").innerHTML = '<p>Nome: '+ data.name + ', Altura:'
//              + data.height + ', peso: ' + data.weight + '</p>';
//              document.getElementById("resultado").innerHTML += 
//              ' "<br><img src="'+data.sprites.front_default +'" width="150">';
//             })

function insiraPokemon(){

    var pokemon = document.getElementById("pokemon").value
        fetch("https://pokeapi.co/api/v2/pokemon/" + pokemon)
        .then(res => res.json())
        .then(data => {
            console.log(data)
            document.getElementById("pokemon-info").innerHTML = '<p>Nome: '+ data.name + ', Altura:' + data.height + ', peso: ' + data.weight + '</p>';
                document.getElementById("pokemon-info").innerHTML += '<br><img src="'+data.sprites.front_default +'" width="150">';
              
            })
            .catch(error => {
     
     fetch("https://api.thedogapi.com/v1/images/search")
    .then(res => res.json())
    .then(data => {
     console.log(data)
         document.getElementById("resultado").innerHTML += "<br><img src='"+data[0].url+"' width = '300px'>";
     })})

    }

     
    </script>
</body>
</html>
