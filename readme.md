# Informações / Anotações do MongoDB
Anotações simples ou avançadas para entender um pouco melhor este banco de dados não relacional,com base nos conhecimentos
aprendidos no curso de MongoDB pela Alura
## Info
O Mongo se parece um pouco com a sintaxe da linguagem *``javascript``*, e é usada como comandos.
Ele cria no lugar de tabelas Uma *Coleção* de dados onde sera manipulada.

## Comandos
* ### ``db.createCollection(coleção)``
    * Irá criar uma coleção,apos isso entre para dentro da coleção para inserir dados

* ### ``db.(suaColeção).insert()``
    * inserção de dados

* ### ``db.(suaColeção).find()``
    * localização/mostrar dados inseridos
    * localização/mostrar de uma maneira espefica podera adicionar o parametro {parametro} para localizar
    *   pretty() - devolve os dados de maneira formatada

* ### `db.(suaColeção).findOne()`
    * Localiza e mostra os dados inseridos de apenas do primeiro registro


   

* ### `db.(suaColeção).update()`

    #### OUR | IN - 
        * {$or:  [{"parametro"},{"parametro"}]}
        * "parametro":{$in:[array] }

    #### SET  - 
    Será necessario passar depois do parametro um *`{$set:{parametro:"nova Informação"}}`* para poder atualizar o dado EX:   
    > `db.(suaColeção).update({"parametro"},{$set:{"campo":"informação"}})`
    
    #### Mult - 
    Por padrao o UPDATE só ira atualizar para o primeiro dado, para atualizar em varios sera necessario utilizar *`{mult:true}`*,
    apos o $set EX:
    > `db.(coleção).update({"parametro"},{$set:{"campo":"informação"}},{multi:true})`

    #### PUSH - 
    Atualizar e cadastrar mais um iten no seu ARRAY sera utilizado o *`$push`* para a inserção de somente 1 dado, EX:
    >`db.(coleção).update({parametro},{ $push:{ARRAY:"nova informação"}})` 

    #### EACH  - 
    Para Inserir varias informações de um ARRAY será utilizado o *`*$each`* EX:
    >`db.(coleção).update({parametro},{ $push:{ARRAY:{$each:[ARRAY]}})` 

    #### GREATER THAN (Maior Que - $gt) - 
    Para poder fazer essa comparação sera necessario usar o seguinte comando *`$gt{parametro}`*, EX:
    >`db.alunos.find({"notas":{$gt:8.5}})`

    #### LESS THAN (Menor que ... - $lt) - 
    Para poder fazer essa comparação será necessario usar o seguinte comando *`$lt{parametro}`*,EX:
    >`db.alunos.find({"notas":{$lt:5}})`

    #### ORDER BY - 
    Usamos para ordenar nossos dados o parametro *`.sort({objeto})`* para fazer essa organização , usamos no exemplo a seguir : 
    >`db.alunos.find().sort({"nome":1})`

    para ordernar o campo nome dos nossos dados com o parametro '1' , esse parametro é equivalente ao ASC nas tabelas SQL , ou seja , será listado os dados cujo o nome esteja em order Alfabetica
    * **1**  - Equivalente ao **ASC**
    * **-1** - Equivalente ao **DESC** 

    #### LIMIT  - 
    Equivalente ao Limite de resultados para ser enviado ao banco de dados,usado ao final do parametro passando o seguinte comando `.limit()`


* ### ``db.(suaColeção).remove({"_id":ObjectId("")})``
    * Remover do banco de dados passando como parametro um id

## Posicionamentos no MongoDB 
Para informar um campo de Localização/Locate na sua coleção,poderá utilizar o seguinte atributo `coordinates:[longitude,latitude]`,porém, após
enviar as coordenadas , é exigido o seguinte atributo `type:string`  para passar um Índice geoespacial .Podem ter diversos indices que são:
* **POINT**
* **LINESTRING**
* **POLYGON**  

Os proprios indices são um pouco autoexplicativos,então não tem muito o que comentar, no curso é usado o Type:Point 

## Buscando por Proximidade
![Aproximação](https://www.azleads.com.br/blog/wp-content/uploads/2019/12/explorar-empresas2-1024x573.png)

* **db.alunos.createIndex({localização:"2dsphere"})** - Será necessario criar uma
busca, para que possamos solicitar uma agregação de valores para a coleção 

* **db.alunos.aggregate()** - após isso será usado este comando para a busca de aggregações , Ex :

```
db.alunos.aggregate([
{ 
    $geoNear:{
        near:{   
            coordinates: [-23.5640265, -46.6527128],
            type:"Point"
        },
        distanceField:"distancia.calculada",
        spherical:true
    }
}
])
```

## Importação
O MongoDB suporta importação de arquivos *`.json`* e para continuar a sessao de posicionamento e buscas por aproximidades foi necessario a importação do arquivo 'alunos.json' que se encontra no projeto.
Para importar basta utilizar o comando 
> ```mongoimport -c alunos --jsonArray < alunos.json```

Feito isso será importado 19 registros/documentos na sua coleção,Para conferir se deu certo basta usar o ``db.alunos.find()``


