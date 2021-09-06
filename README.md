# inventory_control

 TEXTTO RETIRADO DO SIT https://www.luiztools.com.br/post/tutorial-crud-em-node-js-com-driver-nativo-do-mongodb/

<<<<<<< HEAD

    O ARTIGO A BAIXO FOI MONTADO COM BASE NO SIT https://www.luiztools.com.br/post/tutorial-crud-em-node-js-com-driver-nativo-do-mongodb/
    Escrito por Luiz Duarte, O TESXTO ASEGUIR TEM O  ITUITO DE TREINAR E ENTENDER SOBRE AS FERRAMENTAS ABORNDADOS NO MESMO, COM ISSO QUALQUER QUESTÃO REFERENTE A DIRgEITOS AUTORAIS ESTÃO SENDO REFERENCIADAS, SE CASO GOSTAREM DO QUE ESTA SENDO TRASCRITO AQUI, ENTREM NO SIT ORIGINAL PARA ENTENDER MELHOR. Texto Criado e Trascrito Meramente Para questão Didatica sem fins Lucrativos.                                                                                                                                    

=======

   O ARTIGO A BAIXO FOI MONTADO COM BASE NO SIT  https://www.luiztools.com.br/post/tutorial-crud-em-node-js-com-driver-nativo-do-mongodb/   que foi Escrito por Luiz Duarte,O TEXTO  ASEGUIR TEM O  ITUITO DE TREINAR E ENTENDER SOBRE AS FERRAMENTAS ABORNDADOS NO MESMO, COM ISSO QUALQUER QUESTÃO REFERENTE A DIRgEITOS AUTORAIS ESTÃO SENDO REFERENCIADAS, SE CASO GOSTAREM DO QUE ESTA SENDO TRASCRITO AQUI, ENTREM NO SIT ORIGINAL PARA ENTENDER MELHOR. Texto Criado e Trascrito Meramente Para questão Didatica sem fins Lucrativos.
>>>>>>> 6edb8bcb849f840d0d1c35f5d95ac0a9f32c1357
 

 Node.js é uma plataforma que permite a você construir aplicações server-side em JavaScript, já falei disso extensivamente neste artigo.
 MongoDB é um banco de dados NoSQL, orientado a documentos JSON(-like), o mesmo formato de dados usado no JavaScript,além de ser utilizado através de funções com sintaxe muito similar ao JS também,diferente dos bancos SQL tradicionais e também já falei disso extensivamente neste artigo.Vê algo em comum entre os dois? Pois é, ambos tem o JavaScript em comum e isso facilita bastante o uso destas duas tecnologias em conjunto, motivo de ser uma dupla bem frequente para projetos de todos os tamanhos.A ideia deste tutorial é justamente lhe dar um primeiro contato prático com ambos, fazendo o famoso CRUD (Create, Retrieve, Update e Delete).

 Neste artigo você vai ver:

  1 - Configurando o Node.js.
  2 - Configurando o MongoDB.
  3 - Conectando no MongoDB com Node.
  4 - Cadastrando no banco.
  5 - Atualizando clientes.
  6 - Excluindo clientes.
 
 # 1 – Configurando o Node.js
 
 Vamos começar instalando o Node.js: apenas clique no link do site oficial e depois no grande  botão verde para baixar o executável certo para o seu sistema operacional (recomendo a versão LTS).
 Esse executável irá instalar o Node.js e o NPM, que é o gerenciador de pacotes do Node. Uma vez com o NPM instalado, vamos instalar o módulo que será útil mais pra frente. Crie uma pasta para 
 guardar os seus projetos Node no computador (recomendo C:node) e dentro dela, via terminal de comando com permissão de administrador (sudo no Mac/Linux), rode o comando abaixo:

                        
                                                                            
          npm install -g express-generator                               
                                                                        
        
 O Express é o web framework mais famoso da atualidade para Node.js. Com ele você consegue criar aplicações e APIs web muito rápida e facilmente. O que instalamos é o express-generator, um gerador de aplicação de exemplo, que podemo usar via linha de comando, da seguinte maneira:

                      
                                                                            
          express -e --git workshoptdc                                   
                                                                        
        

   O “-e” é para usar a view-engine (motor de renderização) EJS, ao invés do tradicional Jade/Pug. Já o “–git” deixa seu projeto preparado para versionamento com Git. Aperte Enter e o projeto será criado (talvez ele peça uma confirmação, apenas digite ‘y’ e confirme).
Depois entre na pasta e mande instalar as dependências com npm install:

                        
                                                                            
          cd workshoptdc                               
          npm install                                                    
                                                                        
        
        
  Ainda no terminal de linha de comando e, dentro da pasta do projeto, digite:

                      
                                                                            
          npm start                                                      
                                                                        
        
   
   Isso vai fazer com que a aplicação default inicie sua execução em localhost:3000, que você pode acessar pelo seu navegador.

        NAVEGADOR 
                      
                                                                            
             Expless                                                     
              Welcome to Express                                        
        

 
 # 2 – Configurando o MongoDB

   OK, agora que temos a estrutura básica vamos fazer mais alguns ajustes em um arquivo que fica na raiz do seu projeto chamado package.json. Ele é o arquivo de configuração do seu projeto e determina, por exemplo, quais as bibliotecas que você possui dependência no seu projeto. Vamos agora acessar o site oficial do MongoDB e baixar o Mongo. Clique no menu superior em Software > Community Server e busque a versão do Community Server mais recente para o seu sistema operacional. Baixe o arquivo e, no caso do Windows, rode o executável que extrairá os arquivos na sua pasta de Arquivos de Programas, seguido de uma pasta server/version, o que é está ok para a maioria dos casos. Dentro da pasta do seu projeto Node, que aqui chamei de workshoptdc, deve existir uma subpasta de nome data, crie ela agora. Nesta pasta vamos armazenar nossos dados do MongoDB. Pelo prompt de comando, entre na subpasta bin dentro da pasta de instalação do seu MongoDB e digite (no caso de Mac e Linux, coloque um ./ antes do mongod e ajuste o caminho da pasta data de acordo):

                      
                                                                            
          mongod --dbpath c:\node\workshop\data                           
                                                                        
                               

   Isso irá iniciar o servidor do Mongo. Se não der nenhum erro no terminal, o MongoDB está pronto e está executando corretamente.
 Agora abra outro prompt de comando (o outro ficará executando o servidor) e novamente dentro da pasta bin do Mongo, digite:

                      
                                                                            
          mongo                                                           
                                                            
           

   Após a conexão funcionar, se você olhar no prompt onde o servidor do Mongo está rodando, verá que uma conexão foi estabelecida. mongod é o executável do servidor, e mongo é o executável de cliente, que você acabou de conectar.
 Opcionalmente você pode usar ferramentas visuais como o MongoDB Compass, que é gratuita.

  Agora, no console do cliente mongo, digite:

                      
                                                                            
          use workshoptdc                                                 
                                                            
          

   Isso vai fazer com que o terminal se conecte exatamente na base “workshoptdc.” No entanto, ela somente será criada de verdade quando adicionarmos registros nela, o que faremos a partir do próprio cliente para exemplificar.
 Uma de minhas coisas favoritas sobre MongoDB é que ele usa JSON como estrutura de dados, o que significa curva de aprendizagem zero para quem já conhece o padrão. Caso não seja o seu caso, terá que buscar algum tutorial de JSON na Internet antes de prosseguir.
 Vamos adicionar um registro à nossa coleção (o equivalente do Mongo às tabelas do SQL). Para este tutorial teremos apenas uma base de customers (clientes), sendo o nosso formato de dados como abaixo:


                      
                                                                            
               { "_id" : ObjectId("1234"),             
                 "nome" : "luiztools",                 
                 "idade" : 32                          
               }                                                          
         

 O atributo _id pode ser omitido, neste caso o próprio Mongo gera um id pra você. No seu cliente mongo, digite:

                      
                                                                                       
          db.customers.insert({ "nome" : "Luiz", "idade" : 32 })                     
                                                                  
        

   Uma coisa importante aqui: “db” é a base de dados na qual estamos conectados no momento, que um pouco antes havíamos definido como sendo “workshoptdc”. A parte “customers” é o nome da nossa coleção, que passará a existir assim que adicionarmos um objeto JSON nela. Tecle Enter para que o comando seja enviado ao servidor. Se tudo deu certo, uma respostas com “nInserted: 1” (number of inserted) deve aparecer.
 Para ver se o registro foi parar no banco realmente, digite:


                      
                                                                                       
             db.customers.find().pretty()                                            
                                                                  
        

O pretty() no final do comando find() é para identar o resultado, que retornará:

                      
                                                                                       
             { "_id"  : ObjectId("5202b481d2184d390cbf6eca"),     
              "nome"  : "Luiz",                                   
              "idade" : 29                                        
             }                                                    
                                                                  
        

Claro, o seu _id pode ser diferente desse, uma vez que o Mongo irá gerá-lo automaticamente. Isto é tudo que precisamos saber de MongoDB no momento, o que me parece bem fácil, aliás! Para saber mais sobre o MongoDB, Google!

Agora vamos adicionar mais alguns registros no seu console mongo:


        
                                                                                       
             custArray = [{ "nome" : "Fernando", "idade" : 33 },  
                        { "nome" : "Teste", "idade" : 20 }]       
             db.customers.insert(custArray);                      
                                                                  
        
        
   Nesse exemplo passei um array com vários objetos para nossa coleção. Usando novamente o comando db.customers.find().pretty() irá mostrar que todos foram salvos no banco. Agora sim, vamos interagir de verdade com o web server + MongoDB.


# 3 – Conectando no MongoDB com Node

Agora sim vamos juntar as duas tecnologias-alvo deste post!

Precisamos adicionar uma dependência para que o MongoDB funcione com essa aplicação usando o driver nativo. Usaremos o NPM via linha de comando de novo:

           
               npm install mongodb    
           
           
Com isso, uma dependência nova será baixada para sua pasta node_modules e uma novas linha de dependência será adicionada no package.json para dar suporte a MongoDB. Primeiramente, para organizar nosso acesso à dados, vamos criar um novo arquivo chamado db.js na raiz da nossa aplicação Express (workshoptdc). Esse arquivo será o responsável pela conexão e manipulação do nosso banco de dados, usando o driver nativo do MongoDB. Adicione estas linhas:

    
         const mongoClient = require("mongodb").MongoClient;            
         mongoClient.connect("mongodb://localhost")                     
                    .then(conn => global.conn = conn.db("workshoptdc")) 
                    .catch(err => console.log(err))                     
        module.exports = { }                                            
    

Estas linhas carregam o objeto mongoClient  a partir do módulo ‘mongodb’ e depois fazem uma conexão em nosso banco de dados localhost, sendo 27017 a porta padrão do MongoDB. Essa conexão é armazenada globalmente, para uso posterior e em caso de erro, o mesmo é logado no console.

A última linha ignore por enquanto, usaremos ela mais tarde.Agora abra o arquivo www que fica na pasta bin do seu projeto Node e adicione a seguinte linha no início dele:
    
                
     global.db = require('../db');  
    

Nesta linha nós estamos carregando o módulo db que acabamos de criar e guardamos o resultado dele em uma variável global. Ao carregarmos o módulo db, acabamos fazendo a conexão com o Mongo e retornamos aquele objeto vazio do module.exports, lembra? Usaremos ele mais tarde, quando possuir mais valor.

A seguir, vamos modificar a nossa rota para que ela mostre dados vindos do banco de dados, usando esse db.js que acabamos de criar.

Para conseguirmos fazer uma listagem de clientes, o primeiro passo é ter uma função que retorne todos os clientes em nosso módulo db.js (arquivos JS que criamos são chamados de módulos se possuírem um module.exports no final), assim, adicione a seguinte função ao seu db.js (substituindo aquela linha do module.exports que tinha antes):

    
       function findAll() { return global.conn.collection("customers").find().toArray(); }   
       module.exports = { findAll }                                                          
    
 

A consulta aqui é bem direta: usamos a conexão global conn para navegar até a collection de customers e fazer um find sem filtro algum. O resultado desse find é um cursor, então usamos o toArray para convertê-lo para um array e retorná-lo.

Repare na última instrução, ela diz que a nossa função findAll poderá ser usada em outros pontos da nossa aplicação que importem nosso módulo db:
        
    
        module.exports = { findAll }    
    
    
Agora vamos programar a lógica que vai usar esta função. Abra o arquivo ./routes/index.js no seu editor de texto (sugiro o Visual Studio Code).  Dentro dele temos apenas a rota default, que é um get no path raiz. Vamos editar essa rota da seguinte maneira:

    
        / GET home page. /                                                                                               
             router.get('/', async (req, res, next) => {                                                                  
                                                         try {    const docs = await global.db.findAll();                 
                                                         res.render('index', { title: 'Lista de Clientes', docs });       
                                                         }                                                                 
                                                         catch (err) { next(err); }                                       
                                                        });                                                               
    

router.get define a rota que trata essas requisições com o verbo GET. Quando recebemos um GET /, a função de callback dessa rota (aquela com req, res e next) é disparada e com isso usamos o findAll que acabamos de programar. Como esta é uma função assíncrona que vai no banco de dados, precisamos usar a palavra reservada await antes dela, ter um try/catch para tratar seus possíveis erros e o callback do router tem de ter a palavra async antes dos parâmetros da função.
