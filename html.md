# Notas sobre HTML

## Seguridade

### Atributo target en links: probremas de seguridade e rendemento

Case todas as webs teñen ligazóns que se abren en novas pestañas deixando a pestaña orixinal abera. Para isto agrégase ao link o atributo `target="_blank"`. Isto supón un problema porque implica un punto de saída da aplicación propia e un problema de accesibilidade se non se fornecen hints e atributos "aria". O problema é que non podemos asegurar que a páxina externa sexa segura. En todo caso, no temos control sobre ese recurso externo.

O punto crítico é que a páxina externa ten acceso á páxina que a enlaza e pode executar un script malicioso na páxina orixinal. Esta técnica de phising é coñécida com _tab nabbing_ (captura de pantalla). Por exemplo pódese modificar a propiedade `window.opener.location`, onde `opener` é unha referencia á páxina que abriu a segunda.

Ademais o atributo `target="_blank"` ten un impacto negativo no rendemento do navegador porque o acceso ao DOM en múltiples xanelas é síncrono (tabs, windows, iframes) e consumen recursos. 

Unha primeira solución é agregar no link o atributo `rel="noopener noreferer`.

Unha segunda opción é facelo por código, eliminando a referencia a opener.

```javascript
const otherWindow = window.open();
otherWindow.opener = null;
```

Outra estratexia é identificar ligazóns insegurar con antelación agregando regras de linteo.


