// Dados dos produtos (simulando um "banco de dados" simples)
const produtos = [
    { id: 1, nome: "Camiseta Básica", preco: 49.90, imagem: "[Imagem de Camiseta]" },
    { id: 2, nome: "Calça Jeans Skinny", preco: 99.50, imagem: "[Imagem de Calça]" },
    { id: 3, nome: "Vestido Floral", preco: 120.00, imagem: "[Imagem de Vestido]" },
];

const containerProdutos = document.getElementById('produtos-container');
const listaCarrinho = document.getElementById('lista-carrinho');
const totalCarrinhoSpan = document.getElementById('total-carrinho');
let carrinho = [];

// Função para exibir os produtos na página
function exibirProdutos() {
    produtos.forEach(produto => {
        const produtoDiv = document.createElement('div');
        produtoDiv.className = 'produto';
        produtoDiv.style.border = '1px solid #ccc';
        produtoDiv.style.padding = '15px';
        
        produtoDiv.innerHTML = `
            <h4>${produto.nome}</h4>
            <p>Preço: R$ ${produto.preco.toFixed(2)}</p>
            <button onclick="adicionarAoCarrinho(${produto.id})">Adicionar ao Carrinho</button>
        `;
        
        containerProdutos.appendChild(produtoDiv);
    });
}

// Função para adicionar um produto ao carrinho
function adicionarAoCarrinho(produtoId) {
    const produtoSelecionado = produtos.find(p => p.id === produtoId);
    if (produtoSelecionado) {
        carrinho.push(produtoSelecionado);
        atualizarCarrinho();
        alert(`${produtoSelecionado.nome} adicionado ao carrinho!`);
    }
}

// Função para atualizar a visualização do carrinho e o total
function atualizarCarrinho() {
    listaCarrinho.innerHTML = ''; // Limpa a lista atual

    let total = 0;
    carrinho.forEach(item => {
        const itemLista = document.createElement('li');
        itemLista.textContent = `${item.nome} - R$ ${item.preco.toFixed(2)}`;
        listaCarrinho.appendChild(itemLista);
        total += item.preco;
    });

    totalCarrinhoSpan.textContent = total.toFixed(2);
}

// Inicializa a exibição dos produtos quando a página carrega
document.addEventListener('DOMContentLoaded', exibirProdutos);