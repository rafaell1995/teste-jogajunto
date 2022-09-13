# Teste para pessoa desenvolvedora PHP

[← Voltar](README.md).

⚠️ Todas as perguntas são baseadas no **PHP 7.4.28**.

## Exemplo

### 0. Quais os valores de `$a` e `$b` no código abaixo? Por quê?

```php
$a = array_merge(array(1,2), NULL);
$b = array_merge($a, array(3));

var_dump($a);
var_dump($b);
```

> ```
> NULL
> NULL
> ```
> 
> A função `array_merge` retorna `NULL` quando qualquer um dos argumentos não for do tipo `array`. Embora o PHP 7 emita warnings sobre erro no tipo do argumento nem toda instalação está configurada para exibir warnings, logo é importante o desenvolvedor verificar os valores maualmente antes da chamada do `array_merge`, especialmente quando estamos concatenando o retorno de um `array_merge`.
>
> No PHP 8 esse comportamento foi atualizado para emitir um erro, o que ajuda a prevenir problemas.
> 
> ```
> Fatal error: Uncaught TypeError: array_merge(): Argument #2 must be of type array
> ```

## Perguntas

### 1. Qual a diferença entre `echo` e `print`?

> O print é uma função e echo é uma declaração embutida no PHP. 
> Se você colocar print(2) em uma variavel e dar um echo nela logo em seguida, na tela ira aparecer o "1" primeiro e depois o número 2 passado, o 'print' sempre retorna 1 independente do que passar para ele e o 'echo' apenas imprime o valor passado após o comando.

### 2. Qual é a saída do código abaixo? Por quê?

```php
$x = true and false;
var_dump($x);
```

> ```
> bool(true).
> ```
> o recebimento dos valores na variavel $x estão sem chaves, então o "=" precede o operador > and na operação, deixando a variavel $x com o valor true;
> Se fosse assim, ele seria false:

```php
$x = (true and false);
var_dump($x);
```

### 3. Qual é a saída do código abaixo? Por quê?

```php
$x = 5;
$a = array(
    $x++ + $x++,
    $x,
    $x-- - $x--,
    $x,
);

var_dump($a);
```

> ```
> array(4) { [0]=> int(11) [1]=> int(7) [2]=> int(1) [3]=> int(5) }
> ```
> O operador ++ para incrementar tem prioridade em cima do '+' na sequencia, então a operação acontece da seguinte maneira:
>
> ($x++) "$x no momento vale 6" (+ $x) "ele soma com o valor 5 da variavel anteriormente, dando o valor 11". Após isso ele não atribui o segundo incremento '++' na soma.
>
> O segundo incremento da posição [0] do array incrementa o valor de "6" resultado do primeiro incremento para "7" incrementando a segunda vez posição [0] do array, deixando a variavel $x na posição [1] do array com o valor de "7" o decremento se a mesma lógica do incremento, assim "6" - "5" é igual a "1" na posição [2] do array.
>
> a ultima posição volta a ser "5" por causa do segundo decremento de $x.


### 4. Quais serão os valores de `$a` e `$b` após a execução do código abaixo? Por quê?

```php
$a = '1';
$b = &$a;
$b = "2$b";
```

> ```
> 21
> 21
> ```
>
> O & é usado para atribuir o valor da variavel $a e a $b no mesmo endereço de memória, assim alterando $a ou $b os proximos resultados serão os mesmos

### 5. O que são Traits e para que servem? 

> Traits são pedaços de código que servem para reutilização de códigos.
>
> São bem parecidas com classes utilizadas para herança, a diferença é que ela não pode ser instanciada como objeto ou serem extendidas pela classe, somente sendo utilizadas através do:
>
> sendo incorporada no código antes da declaração da classe por meio do import;
>
> `use NomeDaTrait;` após a abertura da classe; 

### 6. Qual será a saída do código abaixo? Por quê?

```php
var_dump(0123 == 123);
var_dump('0123' == 123);
var_dump('0123' === 123);
```


> ```
> bool(false) bool(true) bool(false)
> ```
>
> A interpretação do php por padrão entende que um numero com 4 casas decimais é Octal.
>
> Assim o numero 0123 em Octal não é igual 123.
>
> Já quando você compara com o mesmo número em uma string ele entende como um número decimal 0123 é igual 123.
>
> O comparador "===" é usado para comparar o valor e o tipo.
>
> Já o comparador "==" é usado para comparar apenas o valor e não o tipo dele

### 7. Qual será a saída do código abaixo? Por quê?

```php
$a = '';
$b = 0;
$c = '0a';

var_dump($a == $b);
var_dump($b == $c);
var_dump($c == $a);
```

> (Sua resposta aqui.)

### 8. Qual será o valor de `$x` após a execução do código abaixo? Por quê?

```php
$x = 3 + "15%";
```

> O resultado dá 18, imprimindo o $x com um echo, mas somente aparece o resultado após um erro informando que "15%" não é um valor numérico. `Notice: A non well formed numeric value encountered in PATH\teste\index.php on line 2`
>
> Mas, se você dar um intval("15%") o resultado é 15, o PHP informa um erro mas continuando 
>
> o PHP interpreta "15%" como um valor INT 15 e soma com 3, dando 18.
>
> Assim 
```php
$x = 3 + intval("15%"); 
echo $x; // 18
```
> não aconteceria o erro e daria 18.

### 9. Qual a diferença entre `require_once()` e `include_once()`?

> As duas função requisitam um arquivo, somente uma única vez. Não podendo ser chamado novamente em outra parte do código.
>
> A diferença é que em um caso de erro o `require_once()` para de executar o script, já o `include_once()` informa o erro e continua a execução do PHP.

### 10. Qual será o valor de `$name` após a execução do código abaixo? Por quê?

```php
$name = 'John ';
$name[10] = 'Doe';
```

> (Sua resposta aqui.)

### 11. Qual será a saída do código abaixo? Por quê?

```php
$x = PHP_INT_MAX;
echo gettype($x + 1);
echo (int)($x + 1);

$y = 1.0;
echo is_float($y);
echo gettype($y);
```

> A constante `PHP_INT_MAX` é uma cosntante pré-definida pelo PHP, ela tem o valor do maior inteiro suportado dependendo da arquitetura do sistema que esta executando, 32bits ou 64bits.
>
> No meu caso de 64bits o valor dela é `int(9223372036854775807)`, somando com o 1 o valor fica: `int(9223372036854775807)`
>
> Executando o código da pergunta o primeiro resultado da negativo:
```php
$x = PHP_INT_MAX; // tipo inteiro
// quando o $x + 1 é passado para o gettype(), ele passa a ser float e negativo
echo gettype($x + 1); // -9223372036854775808 tipo double/float
echo (int)($x + 1); //-9223372036854775808
```
> No caso da variavel `$y` o valor 1.0 é um float, ele retorna apenas o '1' na tela por que `is_float()` é uma validação e essa validação é verdadeira, por tanto é 1.

### 12. Qual será o valor de `$x` após a execução do código abaixo? Por quê?

```php
$x = "one" + 1;
```

> Novamente, o `PHP` interpreta a string como inteiro, convertendo a string para 0 e depois somando com "1" é igual a "1".
>
> Mas seguido de um Warning informando que o valor não é numérico.
>
`Warning: A non-numeric value encountered in PATH\teste\index.php on line 3`

### 13. Qual a diferença entre `isset()` e `empty()`?

> O `isset()` informa se a varavel foi iniciada anteriormente no código, ja o `empty()` determina se a variavel é vazia
