# Documentação Back-End

## Desenvolvedores

- <a href = "https://github.com/Andressaffs"> Andressa Ferreira </a>
- <a href = "https://github.com/athosgpm"> Athos Mesquita </a>
- <a href = "https://github.com/Carolguida">Carolina Guida</a>
- <a href = "https://github.com/GUSTAVO-GUILHEN">Gustavo de Souza Guilhen</a>
- <a href = "https://github.com/MariaNazar">Maria Nazare</a>
- <a href = "https://github.com/Velasco18">Osvaldo Velasco</a>
- <a href = "https://github.com/tatiantunes">Tatiane Tissoni</a>

## Sobre
O projeto consiste em uma `Rede Social` voltada para o público de classe média-baixa onde podem expor suas ideias de empreendedorismo e pessoas que gostarem da ideia podem se colabor, seja de forma financeira quanto com serviços prestados.

## Tecnologias principais
- Spring Boot
- Spring Data
- Spring Web
- Spring Security
- Swagger

## Swagger
[Aqui](LINK DO SWAGGER) você pode realizar a consulta da documentação do projeto, bem como realizar requisições por meio de nossos endpoints.

## Tema

 ### Model

| Atributo | Tipo | Qtd. Caracteres |
|----------|------|-----|
| idTema | [PK] long |
| descricaoTema | String | min = 5, max = 255
| categoriaTema | String | min = 5, max = 50
| postagem | List < Postagem > |


| Atributo | Tipo |
|----------|------|
| idTema | [PK] long |
| descricaoTema | String |
| categoriaTema | String |
| postagem | List < Postagem > |

A tabela possuirá os atributos **ID** referente ao código de cada tema e **categoria** onde iremos inserir a temática: tecnologia, meio ambiente, projetos, financiamento, etc. Mais a lista de postagem da marcação @OneToMany.

### CRUD
 
| Métodos | End-points | Descrição |
|----------|--------------|----------|
| Get | /tema | Listar todos os temas existentes
| Get | /tema/{idTema} | Listar tema específico pelo ID
| Get | /tema/categoriaTema/{categoriaTema} | Listar um tema específico pela categoria
| Post | /tema | Inserir os dados
| Put | /tema | Editar algum dado específico
| Delete | /tema/{idTema} | Excluir algum dado pelo ID

A tabela possuirá os end-points básicos (get, post, put e delete) e mais dois métodos específicos, que buscam pelo id e pela categoria.

## Postagem

 ### Model

| Atributo | Tipo | Qtd. Caracteres |
|----------|------|-----|
| idPostagem | [PK] long |
| tituloPostagem | String | min = 5, max = 50
| dataPostagem | Date |
| descricaoPostagem | String | min = 5, max = 255
| urlImagemPostagem | String | min = 5, max = 255
| usuario_id | [FK] long
| tema_id | [FK] long

A tabela possuirá os atributos **idPostagem**, **tituloPostagem**, **dataPostagem**, **descriçãoPostagem** e **urlImagemPostagem** referente a cada postagem, mais as chaves estrangeiras **usuario**  e **tema** onde irão fazer o link com esses.

### CRUD
 
| Métodos | End-points | Descrição |
|----------|--------------|----------|
| Get | /postagens | Listar todas as postagens existentes
| Get | /postagens/{idPostagem} | Listar postagem específica pelo ID
| Get | /postagens/tituloPostagem/{tituloPostagem} | Listar uma postagem específica pelo Título
| Post | /postagens | Inserir os dados
| Put | /postagens | Editar algum dado específico
| Delete | /postagens/{idPostagem} | Excluir algum dado pelo ID

A tabela possuirá os end-points básicos (get, post, put e delete) e mais dois métodos específicos, que buscam pelo id e pelo título.

## ComentarioPostagem

 ### Model

| Atributo | Tipo | Qtd. Caracteres |
|----------|------|-----|
| idComentario | [PK] long |
| comentario | String | min = 0, max = 9999
| usuario_id | [FK] long
| postagem_id | [FK] long

A tabela possuirá os atributos **idComentario** e **comentarios** referente a cada comentário, mais as chaves estrangeiras **usuario**  e **postagem** onde irão fazer o link com esses.

### CRUD
 
| Métodos | End-points | Descrição |
|----------|--------------|----------|
| Get | /comentarios| Listar todos os comentários existentes
| Get | /comentarios/{id} | Listar comentário específico pelo ID
| Post | /comentarios | Inserir os dados
| Put | /comentarios | Editar algum dado específico
| Delete | /comentarios/{id} | Excluir algum dado pelo ID

A tabela possuirá os end-points básicos (get, post, put e delete) e mais um método específico, que busca pelo id.

## Usuário

 ### Model

| Atributo | Tipo | Qtd. Caracteres |
|----------|------|-----------------|
| idUsuario | [PK] long 
| nomeUsuario | String | min = 2, max = 12
| emailUsuario | String | min = 5, max = 100
| senhaUsuario | String |  min = 2, max = 100
| imagemUsuario | String |
| tipoUsuario | String |
| telefoneUsuario | String |

A tabela possuirá os atributos **ID** referente ao código de cada usuário, **nomeUsuario**, **emailUsuario**, **senhaUsuario**, **imagemUsuario**, **tipoUsuario** e **telefoneUsuario**.

### CRUD
 
| Métodos | End-points | Descrição |
|----------|--------------|----------|
| Get | /usuario | Listar todos os usuários existentes
| Get | /usuario/{id} | Listar usuário específico pelo ID
| Post | /usuario/cadastrar | Cadastrar um novo usuário
| Post | /usuario/logar | Logar um usuário existente
| Put | /usuario | Editar algum dado específico

Os caminhos para cadastrar e logar precisam de autenticação por token.

### Model UserLogin (apenas para Login)
| Atributo | Tipo | 
|----------|------|
| nomeUsuario | String |
| emailUsuario | String | 
| senhaUsuario | String |  
| imagemUsuario | String |
| tipoUsuario | String |
| telefoneUsuario | String |
| token | String |

Criada a model ```UserLogin```, que devolve os dados do usuário logado com o token de autenticação.

```UsuarioRepository``` com busca específica para determinado usuário.

Criada a package ```Security``` com as classes ```BasicSecurityConfig```, ```UserDetailsImpl``` e ```UserDetailsServiceImpl```, aplicando as regras de negócio que foram determinadas na interface e restringindo a interação sem autenticação para os caminhos ```"/usuario/cadastrar"``` e ```"/usuario/logar"```.

Criada a package ```Service``` com a classe ```UsuarioService``` que encripta a senha escolhida pelo usuário e guarda no banco de dados.


### Json

#### Enviando dados para cadastrar

```json
{
    "nomeUsuario": "Gustavo",
    "emailUsuario": "Gustavo@gmail.com",
    "senhaUsuario": "123456",
    "tipoUsuario": "Colaborador",
    "telefoneUsuario": "00123451234"
}
```

#### Recebendo dados para logar

```json
{
    "nomeUsuario": "Gustavo",
    "emailUsuario": "Gustavo@gmail.com",
    "senhaUsuario": "123456",
    "tipoUsuario": "Colaborador",
    "telefoneUsuario": "00123451234",     
    "token": "Basic R3VpbGhlbkBnbWFpbC5jb206MTIzNDU2"
}
``` 

