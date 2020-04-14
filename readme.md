# Informações / Anotações do MongoDB
Anotações simples ou avançadas para entender um pouco melhor este banco de dados nao relacional
## Info
O Mongo se parece um pouco com a sintaxe da linguagem `javascript`,e é usada
como comandos.
Ele cria no lugar de tabelas Uma *Coleção* de dados onde sera manipulada.

## Comandos
* db.createCollection(o nome da coleção)
    * Irá criar uma coleção,apos isso entre para dentro da coleção para inserir dados

* db.(suaColeção).insert();
    * inserção de dados

* db.(suaColeção).find();
    * localização/mostrar dados inseridos
    * localização/mostrar de uma maneira espefica podera adicionar o parametro {parametro} para localizar
    *   pretty() - devolve os dados de maneira formatada

* OUR | IN - 
    * {$or:  [{"parametro"},{"parametro"}]} - Comparar se as duas condições sao verdade
    * "parametro":{$in:[array] } 

* db.(suaColeção).update()

    * SET  - Será necessario passar depois do parametro um *`{$set:{parametro:"nova Informação"}}`* para poder atualizar o dado EX:
       
       `db.(suaColeção).update({"parametro"},{$set:{"campo":"informação"}})`
    
    * Mult - Por padrao o UPDATE só ira atualizar para o primeiro dado, para atualizar em varios sera necessario utilizar *`{mult:true}`*,apos o $set EX:
        `db.(coleção).update({"parametro"},{$set:{"campo":"informação"}},{multi:true})`

    * PUSH - Atualizar e cadastrar mais um iten no seu ARRAY sera utilizado o *`$push`* para a inserção de somente 1 dado, EX:
        `db.(coleção).update({parametro},{ $push:{ARRAY:"nova informação"}})` 
        * EACH  - Para Inserir varias informações de um ARRAY será utilizado o *`*$each`* EX:
        `db.(coleção).update({parametro},{ $push:{ARRAY:{$each:[ARRAY]}})` 

* db.(suaColeção).remove({"_id":ObjectId("")})
    * Remover do banco de dados passando como parametro um id
