# Encapsulamento - Modificadores de acesso
> Se nenhum modificador for definido, private será o modificador por padrão
>> A classe mais externa só pode ser public ou global
>>> Conteúdos internos não podem ter acesso menos restritivo que conteúdos externos. Ou seja, um método não pode ser global se a classe for só public, nem public se a classe for private etc.
## Private
- Restringe o acesso das variáveis, funções ou classes para a classe externa. Não poderão ser utilizados fora da classe pai
- As classes internas não terão acesso
   
## Protected
- A classe pai e as classes internas terão acesso, assim como as classes que extendem a classe pai

## Public
- Acesso disponível para todas as classes do Apex no mesmo namespace

## Global
- Acesso para todos
___
# Palavra static
> Os métodos static ou métodos da classe são funções que não dependem de nenhuma variável de instância, quando invocados executam uma função sem a dependência do conteúdo de um objeto ou a execução da instância de uma classe, conseguindo chamar direto qualquer método da classe.
>> Curiosidade: System.debug() é um método estático, pois conseguimos chamá-lo sem instanciar a classe, diretamente pelo próprio nome

```
Exemplo:

public class Fitness {
   
    public static Decimal calculateIMC(Decimal weight, Decimal height) {
        Decimal result = weight / (height * height);
        return result;
    }
    
}

//fora da classe
System.debug(Fitness.calculateIMC(60, 1.72));
```
___
# Polimorfismo
> Quando um método poderá ter mais de uma definição, dependendo do parâmetro que nós fornecermos:
>> Um método pode ter o mesmo nome, desde que o parâmetro seja de tipo diferente. Ex. criaMetodo(String nome) e criaMetodo(Integer number)
___
# This
> A palavra this refere-se à variável global (instância da classe)
```
public static Integer teste = 0;

public method(Integer teste) {
    this.teste = teste;
}

// Observe que neste caso this.teste refere-se à palavra teste fora do método (variável global) e teste refere-se à variável dentro do método (variável local)
```
___

# Construtor x Bloco de inicialização
> O construtor serve para quando você deseja obter o valor do usuário, o bloco de inicialização serve para quando você deseja inicializar valores, sem obtê-los dos usuários

### Construtor exemplo:
```
public class Teste {

    public Integer numero;
    public Integer outroNumero;

public Teste(Integer numero, Integer outroNumero){
    this.numero = numero;
    this.outroNumero = outroNumero;
}

public void metodo(){
    numero++;
    outroNumero++;
}
}
```
### Bloco de inicialização exemplo:
```
public class Teste {

    {
        numero = 1;
        outroNumero = 2;
    }

public void metodo(){
    numero++;
    outroNumero++;
}

}
```