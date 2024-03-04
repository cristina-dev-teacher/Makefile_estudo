# Iniciando um curso de Makefile
Aqui o link do video [clique aqui](https://youtube.com/playlist?list=PLLCFxfe9wkl-tCZvSCbzQGcNv9nSN5ZAP&si=IeODjMlVtgqUI7Hh)
Aqui o link do material na qual o video se baseou [clique aqui](https://www.gnu.org/software/make/manual/make.html)

<br />

## Iniciando o curso video2 [github](https://github.com/Dirack/curso-Makefile)

Temos diretiva de compilação temos a tabuaçao e temos o alvo , isso são regras a serem aplicadas ao programa makefile

Vamso ao codigo ola mundo para ser executado no terminal

```make
# Makefile
# Objetivo: Exibir uma mnsagem de ola mundo
# site: http://www.dirackslounge.online
# Programador: 
# Email:
# Licença:

all:
    echo "Olá mundo, Makefile! :)"
```

Você pode observar que a execução não foi silenciosa pois ele mostrou a função que ia executar e depois executou o comando para evitar coloque o @ antes de echo assim ele só executa o comando.

## video03: 
O makefile precisa ser iniciado de algum momento ele tem as proprias palavras chaves mas podemos escrver as nossas para escrever o codigo primeiro você precia ter um alvo e depois tem os comando mas vamos supor que precise de outras tarefas para poder exeutar seu alvo então você adiciona as dependencias a eles para poder ser executada antes dos comandos abaixo um exemplo de como ficaria

```make
alvo: dependencia
    comando1
    comando2
    .....
dependencia:
    comandos
    ...
# lembre ele executa primiro as dependencias para depois executar os comandos 
```

Tomando como exempo simples podemos ter a flag nativa do makefile que é o all ele executa tudo que esta no script do makefile , mas podemos tambem no prompt mostrar tudo que esta escrto no makefile basta colocar o comando **make -n** ele mostra um print de tudo que esta escrito no makfile e sem executar o makefile, ele ainda coloca na ordem de execuão como se fosse depurar o codigo.
O exemplo abaixo mostra que ele exeuta a dependencia depois os comandos e não executa uma dependencia que não esta ligada a um alvo

```make
# execute este arquivo como: make -n
all: sou_dependente
    @echo "Faço parte da flag all e vou ser executada depois"

sou_dependente:
    @echo "Sou uma dependencia e vou ser executada primeira"

# para executar esta dependencia basta: make nao_dependo
nao_dependo:
    @echo "Não vou aparecer no prompt pois ninguem me chamou"

```

## video04: aula 03 

Vamos definir algumas perguntas para construir corretamente um arquivo makefile
alvo:   dependencia
    comando
alvo: o que sera produzido   
dependencia: do que eu preciso para produzir o alvo  
comando: como a partir da dependencia vou produzir o alvo  

No exemplo mostrado tem arquivos para compilação mas é feito em fortran e não tenho este sistema para fazer este comando , mas escreverei aqui para ver como ele ficou

```make
# Makefile
programa.x:     programa.f90 modulo_lib.o
    gfortran modulo_lib.o programa.f90 -o programaxxx.x
modulo_lib.o:   modulo_lib.f90
    gfortran -c modulo_lib.f90

# Como este exige um sitema faça o mesmo somente com C a soma de dois numeros
```

## video05: aula 04 => Remover arquivos com Make Clean
Para remover ele usou um comando do proprio shell do linux para fazer a remoção destes arquivos no caso ele colocaou tambem um novo alvo chamado clean abaixo o exemplo do que ele fez

```make
# Makefile

programa.x:     programa.f90 modulo_lib.o
    gfortran modulo_lib.o programa.f90 -o programa.x

modulo_lib.o:   modulo_lib.f90
    gfortran -c modulo_lib.f90

clean:
# Aqui ele exclui todos os arquivos com extençao .o e .mod
    rm *.o
    rm *.mod
```
Para aplicar o clean e reover os arquivos basta fazer **make clean**

## video06: aula 05, flags para compilação
No nosso caso vou colocar somente referente a linguagem C

Para a linguagem C, as opções `-c`, `-o`, `-j`, e `-I` são usadas no compilador GCC para controlar o processo de compilação e vinculação. Vou explicar cada uma delas com detalhes:

- **`-c`**: Esta opção instrui o compilador a compilar os arquivos de origem em arquivos de objeto, mas não a vincular esses arquivos de objeto em um executável. Isso é útil quando você deseja compilar arquivos de origem individualmente antes de vincular todos os arquivos de objeto juntos em um único executável. Em outras palavras, `-c` permite que você gere arquivos de objeto `.o` sem criar um executável diretamente, o que pode ser útil em projetos de compilação complexos onde a vinculação é feita separadamente [3].

- **`-o`**: A opção `-o` é usada para especificar o nome do arquivo de saída. Ela é seguida pelo nome que você deseja dar ao arquivo de saída. Por exemplo, `gcc -o meu_programa meu_programa.c` compilará o arquivo `meu_programa.c` em um executável chamado `meu_programa`. Isso permite que você controle o nome do executável gerado, em vez de usar o nome padrão baseado no nome do arquivo de origem [3].

- **`-j`**: A opção `-j` não é uma opção padrão do GCC para C. No entanto, em alguns contextos, `-j` pode ser usado para especificar o número de processos simultâneos que o compilador pode usar durante a compilação, o que pode acelerar o processo de compilação em sistemas com múltiplos núcleos de CPU. Esta opção é mais comumente encontrada em compiladores de outras linguagens, como o GCC para C e C++, e seu comportamento pode variar dependendo do compilador e da versão.

- **`-I`**: A opção `-I` é usada para especificar diretórios adicionais onde o compilador deve procurar arquivos de cabeçalho (`.h`) durante a compilação. Isso é útil quando os arquivos de cabeçalho não estão no diretório de trabalho atual ou em qualquer um dos diretórios padrão que o compilador verifica automaticamente. Por exemplo, `gcc -I/caminho/para/cabecalhos meu_programa.c -o meu_programa` instrui o compilador a incluir o diretório `/caminho/para/cabecalhos` na busca por arquivos de cabeçalho, permitindo que o compilador encontre e use esses arquivos durante a compilação do `meu_programa.c` [3].

Essas opções permitem um controle mais fino sobre o processo de compilação, facilitando a construção de projetos complexos, a otimização do processo de compilação em sistemas com múltiplos núcleos, e a organização de arquivos de código e cabeçalho em projetos C.
