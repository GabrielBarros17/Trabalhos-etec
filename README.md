<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
<title>Planejamento para a festa</title>
<style>
    html, body {
        height: 100%; /* Garantir que o body ocupe 100% da altura da viewport */
        margin: 0; /* Remover margens padrão */
    }
    body {
        display: flex;
        flex-direction: column;
        background: linear-gradient(135deg, #6a1b9a, #b00b69); /* Gradiente de roxo para rosa */
    }
    .content {
        flex: 1; /* Permitir que o conteúdo ocupe o espaço disponível */
    }
    .modal-content {
        background: #343a40; /* Fundo escuro para o modal */
        color: white; /* Texto branco para o modal */
    }
    .footer {
        background: rgba(0, 0, 0, 0.2); /* Cor de fundo semi-transparente para o footer */
        color: white;
    }
    .modal-body {
        text-align: center; /* Centralizar o texto no modal */
    }
    .modal-body img {
        display: block;
        margin: 0 auto; /* Centralizar a imagem no modal */
        max-width: 100%;
        height: auto; /* Manter a proporção da imagem */
    }
</style>
</head>
<body>
    <div class="content">
        <center>
            <a href="Lista da Festa.html" class="btn button bg-dark">Teste</a>
            <div class="rounded-5 container-sm w-50 bg-dark text-white">
                <h1 class="mt-5">Lista para a festa</h1>
                <div class="container text-center mt-1">
                    <div class="row">
                        <div class="col">
                            <h3 class="mb-4">Adicionar Informações para a festa</h3>
                            <form id="formItem">
                                <div class="row mb-2">
                                    <div class="col">
                                        <label for="inputPrimeiroNome" class="fw-bold">Primeiro Nome</label>
                                        <input type="text" id="inputPrimeiroNome" class="form-control text-center" placeholder="Primeiro Nome" required>
                                    </div>
                                    <div class="col">
                                        <label for="inputUltimoNome" class="fw-bold">Último Nome</label>
                                        <input type="text" id="inputUltimoNome" class="form-control text-center" placeholder="Último Nome" required>
                                    </div>
                                </div>
                                <label for="inputDescricao" class="fw-bold">Sua idade e Presente</label>
                                <input type="text" id="inputDescricao" class="mb-1 text-center form-control w-100" placeholder="Idade e descrição do presente" required>
                                <label for="inputImagem" class="fw-bold">Foto do Presente</label>
                                <input type="file" id="inputImagem" class="mb-1 text-center form-control w-100" accept="image/*" required>
                                <button class="btn btn-danger mt-2" type="submit">Adicionar</button>
                            </form>
                        </div>
                        <ul class="list-group mt-4" id="listaItens">
                            <!-- Lista de itens será adicionada aqui -->
                        </ul>
                    </div>
                </div>
            </div>

            <!-- Modal -->
            <div class="modal fade" id="modalItem" tabindex="-1" aria-labelledby="modalItemLabel" aria-hidden="true">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title" id="modalItemLabel">Título do Item</h5>
                            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                        </div>
                        <div class="modal-body">
                            <p id="modalDescricao">Descrição do item</p>
                            <img id="modalImagem" src="" alt="Imagem do item" class="img-fluid">
                        </div>
                    </div>
                </div>
            </div>
        </center>
    </div>

    <footer class="d-flex flex-wrap justify-content-between align-items-center fixed-bottom border-white border-top footer">
        <div class="d-flex align-items-center">
            <a href="/" class="mb-3 me-2"></a>
            <span class="text-white">Jhonnatan Paulino Nº19 & Gabriel Souza Nº17</span>
        </div>
    </footer>

    <script>
        document.getElementById('formItem').addEventListener('submit', function(event) {
            event.preventDefault();

            var primeiroNome = document.getElementById('inputPrimeiroNome').value.trim();
            var ultimoNome = document.getElementById('inputUltimoNome').value.trim();
            var descricao = document.getElementById('inputDescricao').value.trim();
            var imagemInput = document.getElementById('inputImagem');
            
            if (primeiroNome !== '' && ultimoNome !== '' && descricao !== '' && imagemInput.files.length > 0) {
                var lista = document.getElementById('listaItens');

                // Lendo o arquivo de imagem
                var imagemFile = imagemInput.files[0];
                var reader = new FileReader();

                reader.onload = function(e) {
                    var imagemDataURL = e.target.result;

                    // Criando o novo item de lista (li)
                    var novoItem = document.createElement('li');
                    novoItem.classList.add('list-group-item', 'd-flex', 'justify-content-between', 'align-items-center', 'mb-1', 'w-50', 'mx-auto');

                    // Criando o link
                    var link = document.createElement('a');
                    link.href = '#';
                    link.textContent = `${primeiroNome} ${ultimoNome}`;
                    link.classList.add('btn', 'mx-auto', 'px-5',);

                    // Adicionando evento ao link para abrir o modal
                    link.addEventListener('click', function(event) {
                        event.preventDefault();
                        document.getElementById('modalItemLabel').textContent = `${primeiroNome} ${ultimoNome}`;
                        document.getElementById('modalDescricao').textContent = descricao;
                        document.getElementById('modalImagem').src = imagemDataURL;
                        var modal = new bootstrap.Modal(document.getElementById('modalItem'));
                        modal.show();
                    });

                    // Adicionando link ao novoItem
                    novoItem.appendChild(link);

                    // Criando botão de remover
                    var botaoRemover = document.createElement('button');
                    botaoRemover.textContent = 'Remover';
                    botaoRemover.classList.add('btn', 'btn-danger', 'btn-sm', 'ms-2');
                    botaoRemover.type = 'button'; // Garantindo que o botão não envie o formulário
                    botaoRemover.onclick = function() {
                        lista.removeChild(novoItem);
                    };

                    // Adicionando botão de remover ao novoItem
                    novoItem.appendChild(botaoRemover);

                    // Adicionando novoItem à lista
                    lista.appendChild(novoItem);

                    // Limpando os campos do formulário
                    document.getElementById('formItem').reset();
                };

                // Ler o arquivo como URL de dados
                reader.readAsDataURL(imagemFile);

            } else {
                alert('Por favor, preencha todos os campos.');
            }
        });
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.8/dist/umd/popper.min.js" integrity="sha384-I7E8VVD/ismYTF4hNIPjVp/Zjvgyol6VFvRkX/vR+Vc4jQkC+hVqc2pM8ODewa9r" crossorigin="anonymous"></script>
</body>
</html>
