# Tyler

> Uma biblioteca de CSS para os sites de Arezzo&Co.

**Futuro:** O manual de estilos de Arezzo&Co.

O Tyler serve para unificar o código CSS entre os sites, para que elementos comuns entre eles compartilhem do mesmo código.

Ter componentes bem definidos, testados e compatíveis para serem facilmente utilizados.

## História

Começou com componentes CSS para uma página Amp e para mostrar os esses componentes foi feito um guia de estilos bem simples.

Concordamos em reunião de criar um CSS comum e um Guia de estilos com componentes, que o nome dele seria Tyler e que todo CSS dele seria prefixado para não conflitar com os já existentes ou de terceiros.

Na estratégia inicial a marcação de todas as marcas teria o mesmo seletor, porém com o código CSS era totalmente separado. A ideia era que o Tyler fosse uma "assinatura" de seletores, onde cada marca deveria fazer do seu jeito. O guia de estilos nessa época assumia que cada marca teria os seus componentes únicos, então lá também cada lista de componentes era separada. Os problemas dessa época era que para colocar no guia de estilos precisava ir marca por marca e para termos os componentes em cada marca tínhamos que copiar o código de outra... A manutenção ficou pesada.

Copiamos a forma como o Bootstrap trabalha de criar variáveis com valores padrões para serem sobrescritas por cada um que fosse usar, no nosso caso as marcas. Dessa forma não temos duplicação de código e facilita muito a replicação para novas marcas.

## O Tyler

O Tyler é baseado em componentes e não em helpers, isso por que não teremos valor definitivos como um texto negrito e sim dizer que ele é um título e cada marca dizer como faz o seu. Por exemplo:

Componentes (correto)

**marcação comum**
```html
<h1 class="ty-tytle">Título</h1>
```

**css Schutz**
```css
.ty-title {
  font-size: 24px;
  fon-weight: bold;
}
```

**css Birman**
```css
.ty-title {
  font-size: 22px;
  fon-weight: normal;
}
```

Helpers (errado)

```html
<h1 class="text-bold text-large">Título</h1>
```

Com helper é muito mais prático, no exemplo acima não atenderia todas as marcas e não seria semântico dizer que um texto é bold e depois sobrescrever na marca.

### Estrutura

- **common** o que será aplicado além do Tyler, são resets, fonts, variáveis CSS nativas...
- **components** seguimos o atomic design
  - 
- **helpers** css que faz o trabalho de estilo em linha. Raramente usado, pois optamos pela estratégia de componentes
- **utilities** SCSS que nunca gera CSS, ou seja, variáveis (SCSS apenas, não CSS), placeholders e mixins

### Forma de trabalhar

Dívidido em Tyler comum e Tyler da marca. As marcas tanto podem sobrescrever as variáveis como o CSS.

Todo layot deve começar a ser escrito pelos elementos menores, para que um componente maior não as propriedades dele e gera um grande acoplamento. O menor componente será um átomo, isso não quer dizer o seu tamanho em tela, mas o CSS que irá conter nele. Um container é um átomo, pois não estiliza nenhum outro.

**átomo**
```scss
.ty-box {
  padding: 20px;
  background-color: antiquewhite;
}

.ty-button {
  padding: 10px;
  background-color: black;
}
```

**molécula**

```scss
.ty-modal {
  ty-box {
   background-color: white;
  }
  
  .ty-button {
    border-radius: 50%;
  }
}
```

## Guia de estilos

[![image](https://user-images.githubusercontent.com/27368585/99832621-9654b580-2b3f-11eb-92b4-93c4d19b53e1.png)](https://tyler.surge.sh/)

O CSS para o guia de estios é especialmente feito para não "vazar", onde todo ele está dentro do seletor `[data-tyler="root"]`. Por exemplo `[data-tyler="root"] .ty-button`. Assim ele tem os 2 mecanismos de defesa:
- prefixo `ty-` que evita do CSS externo afetar os componentes
- seletor específico com `[data-tyler="root"]` para que o CSS do componente não afete os do guia de estilos. 

## Futuro

### Guia de estilos no front-vendors

Vantagens:

- não precisa subir a hybris para testar
- rodar automaticamente o comando deploy no jenkins (Guia sempre atualizado)
- fica próximo do dev
- possível rodar testes e linters nele
- PR mais visto
- Processo natural de aprovação de PR, testes, deploy...

### Limpeza do CSS Tyler antigo

A ideia antiga de copiar o CSS para cada marca ainda tem resquícios e geralmente atrapalha no desenvolvimento, pois é um código repetido que sobrescreve o do Tyler comum.
