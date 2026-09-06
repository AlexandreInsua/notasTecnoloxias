# VIEW ENCAPSULATION DE ANGULAR

Claro, a información que tes está orientada a unha explicación xeral, pero para **Angular 19 e seguintes**, o tema de encapsulación de estilos é fundamental e moi específico. Vou transformar o teu documento para que sexa unha guía técnica avanzada enfocada nas estratexias de encapsulación que ofrece Angular 19, integrando o que aprendemos sobre CSS Nesting e `:host-context` no contexto correcto.

---

## 1. O Motor de Encapsulación en Angular 19

Cada compoñente de Angular ten unha configuración de encapsulación de estilos que determina como o framework escapa os estilos . Esta configuración é fundamental para evitar conflitos CSS entre compoñentes e o resto da aplicación.

### 1.1. Os catro modos de encapsulación

Angular 19 ofrece catro modos principais, cada un coas súas consecuencias técnicas:

| Modo                                                  | Comportamento                                                                                                                                                                                                                                 | Cando usalo?                                                                                                                    |
| :---------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------ |
| **`ViewEncapsulation.Emulated`** (Por defecto)        | O compilador de Angular xera atributos HTML únicos (como `_ngcontent-ng-c885857805`) e os aplica aos selectores CSS . **Non usa Shadow DOM nativo**, senón que imita o comportamento. É o modo máis seguro e con menor impacto no rendemento. | Para a maioría dos compoñentes da aplicación.                                                                                   |
| **`ViewEncapsulation.ShadowDom`**                     | Usa a API nativa de Shadow DOM do navegador. Crea unha "sombra" arredor do compoñente que bloquea completamente os estilos externos .                                                                                                         | Cando necesitas un illamento total e queres usar Web Components. Require coñecer as implicacións de eventos e slots.            |
| **`ViewEncapsulation.ExperimentalIsolatedShadowDom`** | Comportamento idéntico ao `ShadowDom`, pero garante estritamente que os estilos globais non poidan afectar ao compoñente .                                                                                                                    | Para compoñentes embebidos en aplicacións de terceiros onde un CSS hostil (con `!important`) non debe romper o teu compoñente . |
| **`ViewEncapsulation.None`**                          | Desactiva toda a encapsulación. Os estilos do compoñente son globais e poden afectar a calquera elemento da aplicación .                                                                                                                      | Úsase só para compoñentes que definen estilos globais ou cando se quere un control manual total. É o modo máis arriscado.       |

### 1.2. Optimización en Produción en Angular 19

Un cambio importante en Angular 19 é a optimización de compoñentes con estilos baleiros. Se un compoñente non ten estilos ou CSS files, Angular 19 establece a encapsulación a `None` en builds de produción para eliminar atributos innecesarios do HTML e reducir o traballo de runtime . Isto é especialmente beneficioso para proxectos con frameworks CSS como Tailwind, onde os estilos se xestionan globalmente.

---

## 2. Estilos Contextuais: `:host` e `:host-context`

Cando usas a encapsulación `Emulated`, Angular soporta pseudo-clases que non dependen do Shadow DOM nativo.

### 2.1. `:host`

Permite estilizar o elemento host do compoñente . É o lugar perfecto para definir variables de CSS propias do compoñente.

```typescript
// styles.css do compoñente
:host {
    display: block;
    background-color: var(--rdr-color-bg, #fff); // Define con fallback
}
```

### 2.2. `:host-context()`

Esta é a peza crave para a tematización. Aínda que os navegadores a deprecaron, **Angular a soporta completamente grazas ao seu compilador** . Permite aplicar estilos ao compoñente baseándose en calquera clase ou atributo presente nos seus devanceiros, ata o `body` .

```typescript
// Aplica un tema escuro se o elemento <body> ten a clase .tema-escuro
:host-context(.tema-escuro) {
    --cor-fundo: #222;
    --cor-texto: #fff;
}

// Aplica estilos específicos se o pai directo ten unha clase
:host-context(.clase-especial) {
    border: 1px solid red;
}
```

---

## 3. Estratexias de Tematización e SCSS en Angular 19

A xestión de temas é un dos retos máis comúns. En Angular 19 hai dúas estratexias claramente diferenciadas:

### 3.1. Estratexia con CSS Custom Properties (Recomendada)

A solución máis robusta e estándar. Defines variables en `:root` no teu `styles.scss` global e as consomes nos compoñentes .

```scss
/* styles.scss (Global) */
:root {
  --mi-color-primario: #9d9dcc;
  --mi-color-secundario: #d3d3ff;
}

/* Compoñente (estilos encapsulados) */
:host {
  background-color: var(--mi-color-primario); // Accede en runtime
}
```

Esta estratexia é ideal porque funciona en calquera modo de encapsulación e non require `::ng-deep`.

### 3.2. Estratexia con Variables SCSS e `:host-context`

Podes usar variables de SCSS para xerar múltiples regras `:host-context` para temas diferentes .

```scss
/* theme.scss */
$theme-dark-bg: #222;
$theme-light-bg: #fff;

/* Compoñente */
:host-context(.tema-escuro) {
  background-color: $theme-dark-bg;
}

:host-context(.tema-claro) {
  background-color: $theme-light-bg;
}
```

**⚠️ Lembrete técnico:** As variables de SCSS (`$var`) resólvense en tempo de compilación, mentres que as CSS Custom Properties (`var(--x)`) son dinámicas en runtime. Se intentas mesturalas, asegúrate de que as rutas de importación de SCSS estean configuradas en `angular.json` para evitar erros de resolución .

---

## 4. `::ng-deep` vs. Alternativas Modernas

`::ng-deep` é unha API legada que Angular desaconsella enerxicamente para novos desenvolvementos . Desactiva a encapsulación a partir de ese punto, convertendo os estilos en globais.

Para evitar `::ng-deep` ao estilizar compoñentes de terceiros (como Angular Material), as alternativas modernas son:

1.  **Métodos globais con clases de contexto:** Engade unha clase ao elemento raíz da ruta e define os overrides no CSS global.
    ```scss
    // Global styles
    .clase-para-ruta-dashboard {
      @include mat.button-overrides(
        (
          filled-container-color: orange,
        )
      );
    }
    ```
2.  **Uso de variables CSS:** Configura as variables de tema de Angular Material no `:root` para que os compoñentes as consuman automaticamente.

---

## 5. Cadro de Decisión: Que estratexia usar?

Esta táboa resume cando empregar cada técnica en Angular 19:

| Escenario de uso                                             | Ferramenta recomendada                            | Por que?                                                                                                         |
| :----------------------------------------------------------- | :------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------- |
| **Aillamento básico de estilos dun compoñente**              | `ViewEncapsulation.Emulated`                      | É o default, rápido e mantén o tamaño do HTML baixo grazas ás optimizacións de v19 .                             |
| **Tematizar un compoñente según un contexto global**         | `:host-context()` + CSS Variables                 | É a forma máis limpa en Angular. O compilador o transforma en atributos, evitando problemas de compatibilidade . |
| **Compoñente embebido en app de terceiros**                  | `ViewEncapsulation.ExperimentalIsolatedShadowDom` | Bloquea completamente o CSS do host, mesmo con `!important` .                                                    |
| **Compoñente con estilos que deben ser globais (ex: reset)** | `ViewEncapsulation.None`                          | Úsase só para casos moi específicos e controlados.                                                               |
| **Estilizar fillos proxectados (slots)**                     | `::slotted()`                                     | É a forma nativa para Shadow DOM. Úsase con `ViewEncapsulation.ShadowDom`.                                       |
