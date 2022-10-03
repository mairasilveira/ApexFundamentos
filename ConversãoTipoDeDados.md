## Converter String para valor numérico
```
Integer mark = Integer.valueOf('85');
```

>Exemplo
```
String notaFisica = '6';
String notaMatematica = '10';
String notaPortugues = '9';

Integer totalSimulado = Integer.valueOf(notaFisica) + Integer.valueOf(notaMatematica) + Integer.valueOf(notaPortugues);
```

## Converter valor numérico para String
```
String.valueOf();
```
> Exemplo
```
Integer nota = 10;

String.valueOf(nota);