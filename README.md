# Tyler

> Uma biblioteca de CSS para os sites de Arezzo&Co.

O Tyler serve para unificar o código CSS entre os sites, para que elementos comuns entre eles compartilhem do mesmo código.

Ter componentes bem definidos, testados e compatíveis para serem facilmente utilizados.

## História

Começou com componentes CSS para uma página Amp e para mostrar os esses componentes foi feito um guia de estilos bem simples.

Concordamos em reunião de criar um CSS comum e um Guia de estilos com componentes, que o nome dele seria Tyler e que todo CSS dele seria prefixado para não conflitar com os já existentes ou de terceiros.

Na estratégia inicial a marcação de todas as marcas teria o mesmo seletor, porém com o código CSS era totalmente separado. A ideia era que o Tyler fosse uma "assinatura" de seletores, onde cada marca deveria fazer do seu jeito. O guia de estilos nessa época assumia que cada marca teria os seus componentes únicos, então lá também cada lista de componentes era separada. Os problemas dessa época era que para colocar no guia de estilos precisava ir marca por marca e para termos os componentes em cada marca tínhamos que copiar o código de outra... A manutenção ficou pesada.

```html
<button class="ty-button">
  um botão
</button>
```

**arezzo**
```css
.ty-button {
  padding: 10px;
  border-radius: 5px;
  background-color: green;
  min-width: 120px;
}
```

**fiever**
```css
.ty-button {
  padding: 10px;
  border-radius: 0;
  background-color: black;
  min-width: 120px;
}
```

Copiamos a forma como o Bootstrap trabalha de criar variáveis com valores padrões para serem sobrescritas por cada um que fosse usar, no nosso caso as marcas. Dessa forma não temos duplicação de código e facilita muito a replicação para novas marcas.

## Benefícios

- Facilita para replicar
- Menos código
- Mais compatível com os navegadores
- Código padronizado
- Fácil de visualizar os componentes disponíveis

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

Os nossos componentes são feitos com Atomic Design e BEM, segue 3 documentos que podem auxiliar:

- [Atomic Design](https://github.com/jomarcardoso/dojo-AtomicDesign)
- [Componentes CSS](https://github.com/jomarcardoso/dojo-css-components)
- [Atomic Design + BEM](https://github.com/jomarcardoso/dojo-atomic-and-bem)

### Estrutura

- **common** o que será aplicado além do Tyler, são resets, fonts, variáveis CSS nativas...
- **components** seguimos o atomic design
  - atoms
  - molecules
  - organisms
  - templates
  - pages
- **helpers** css que faz o trabalho de estilo em linha. Raramente usado, pois optamos pela estratégia de componentes
- **utilities** SCSS que nunca gera CSS, ou seja, variáveis (SCSS apenas, não CSS), placeholders e mixins

### Forma de trabalhar

Planejar para:

- ver se o componente não existe ou se não da para modificar algum para atender
- ver o que é reaproveitável para componentizar
- colocar nomes bons

Exemplos de tarefas:

- [Componentes átomos do chekout](https://github.com/ArezzoCo/ecommerce-hybris/issues/10784)
- [Componentes moléculas do checkout](https://github.com/ArezzoCo/ecommerce-hybris/issues/10789)
- [Componentes templates do checkout](https://github.com/ArezzoCo/ecommerce-hybris/issues/11003)
- [Componentes úteis Trocas e devoluções](https://github.com/ArezzoCo/ecommerce-hybris/issues/15346)

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

### Guia de estilos no front-vendors

Vantagens:

- não precisa subir a hybris para testar
- rodar automaticamente o comando deploy no jenkins (Guia sempre atualizado)
- fica próximo do dev
- possível rodar testes e linters nele
- PR mais visto
- Processo natural de aprovação de PR, testes, deploy...
- usar também componentes React

### Limpeza do CSS Tyler antigo

A ideia antiga de copiar o CSS para cada marca ainda tem resquícios e geralmente atrapalha no desenvolvimento, pois é um código repetido que sobrescreve o do Tyler comum.

### Ser um manual de estilos de Arezzo&Co.

Os designers olharem lá para verem cores, fontes, componentes, espaçamentos... Inclusive contribuirem com o que tem lá para tornar-se a nossa referência dos estilos.

Cada nova marca poderá ter seus componentes vistos antes mesmo de ser implementada.

# Testando conhecimentos e praticando

Vimos que a página é o componente mor, olhando o carrinho com e sem produtos, ambas são o mesmo componente?

![image](https://user-images.githubusercontent.com/27368585/99838604-2b5bac80-2b48-11eb-882c-a56df8a6beed.png)
![image](https://user-images.githubusercontent.com/27368585/99838692-4c240200-2b48-11eb-8ab8-e735d4cd8af3.png)

## Criar uma nova marca

Para testar vamos copiar o theme do Tyler comum para alme. Algumas ideias:

- [![image](https://user-images.githubusercontent.com/27368585/99847077-42090000-2b56-11eb-86c8-fb8f702d1ead.png)
](https://coolors.co/ff6b35-f7c59f-efefd0-004e89-1a659e)
- font-family verdana ou tahoma (acho que ainda não vai dar isso)
- botões levemente arredondados (2px)
- títulos bem salientes

## Criar o componente de botão de natal

![image](https://user-images.githubusercontent.com/27368585/99967857-2761a180-2d77-11eb-86fe-b1fdd996abbc.png)

# Perguntas e afirmações frequentes

> Isso daqui será usado só uma vez preciso fazer um componente?

Você sabe do futuro? Será mesmo que será usado apenas uma vez?

> Não vou fazer componente porque não é reaproveitável.

Se quebrar esse teu componente em partes menores, essas partes não podem ser usadas em outros lugares?

Como vimos no Atomic Design tudo é componente, ser reaproveitável vai da mão do dev.

> Esse componente só será usado em uma marca, vou fazer ele especificamente lá

Assim como o Bootstrap o Tyler é uma coleção de componentes e que nem todos serão usados em todos os lugares.
