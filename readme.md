# Informações / Anotações do MongoDB
Anotações simples ou avançadas para entender um pouco melhor este banco de dados nao relacional
## Info
O Mongo se parece um pouco com a sintaxe da linguagem `javascript`,e é usada
como comandos.
Ele cria no lugar de tabelas Uma *Coleção* de dados onde sera manipulada.

### Comandos
* db.createCollection(o nome da coleção)
    * Irá criar uma coleção,apos isso entre para dentro da coleção para inserir dados
    
* db.(suaColeção).insert();
    * inserção de dados

* db.(suaColeção).find();
    * localização/mostrar dados inseridos
    * localização/mostrar de uma maneira espefica podera adicionar o parametro {parametro} para localizar
    *   pretty() - devolve os dados de maneira formatada

* OUR | IN - 
    * {$or:  [{"parametro"},{"parametro"}]}
    * "parametro":{$in:[array] }

* db.(suaColeção).remove({"_id":ObjectId("")})
    * Remover do banco de dados passando como parametro um id