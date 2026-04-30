# festival

Descreva aqui as alterações/correções que fez


### Explicação da linha `ordering = ["dia__data", "hora"]` no `models.py`

A instrução `ordering = ["dia__data", "hora"]`, colocada dentro da classe `Meta` de um modelo Django (neste caso, no modelo `Concerto`), serve para definir a **ordenação padrão** (default ordering) dos registos sempre que fazemos uma consulta à base de dados.

Esta lista diz ao Django para ordenar os resultados aplicando os seguintes critérios, por ordem de prioridade:

1. **`"dia__data"` (Critério Principal):** O duplo underscore (`__`) é a sintaxe do Django para navegar por relações de chaves estrangeiras (*Foreign Keys*). Aqui, diz ao Django para ir ao modelo `Dia` (através do campo `dia` do concerto) e ordenar os resultados pela `data` de forma crescente. Isto garante que os concertos do primeiro dia do festival aparecem primeiro.
2. **`"hora"` (Critério Secundário):** Como há vários concertos no mesmo dia, o Django precisa de um segundo critério de ordenação. O campo `"hora"` garante que, dentro do mesmo dia, os concertos aparecem por ordem cronológica.

**O que acontece se retirar a linha?**
Se remover esta linha de código, o Django perde a instrução de ordenação. Por consequência, os concertos passarão a ser devolvidos e mostrados na página web de forma aparentemente aleatória ou pela ordem em que foram criados na base de dados (ordenados pelo `ID`), destruindo a organização do horário do festival.

**O que acontece se alterar a linha?**
* Se alterar para `ordering = ["hora"]`: O Django vai ignorar os dias. Vai mostrar o concerto das 17h do dia 2, seguido do concerto das 18h do dia 1, etc., misturando os dias todos.
* Se adicionar um sinal de menos (`-`), como em `ordering = ["-dia__data", "-hora"]`: A ordenação passa a ser decrescente. O site começaria por mostrar os concertos do último dia do festival, a começar pelo mais tardio até ao mais cedo.