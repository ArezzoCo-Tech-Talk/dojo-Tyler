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

## Guia de estilos

[![image](https://user-images.githubusercontent.com/27368585/99832621-9654b580-2b3f-11eb-92b4-93c4d19b53e1.png)](https://tyler.surge.sh/)

## Futuro

### Guia de estilos no front-vendors

Vantagens:

- não precisa subir a hybris para testar
- rodar automaticamente o comando deploy no jenkins (Guia sempre atualizado)
- fica próximo do dev
- possível rodar testes e linters nele
- PR mais visto
- Processo natural de aprovação de PR, testes, deploy...
