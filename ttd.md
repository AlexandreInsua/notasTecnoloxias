# TDD

## 1. Axilismo

O axilismo aparece como resposta aos problemas do desenvolvemento en cascada. Trátase dunha declaración de principios mais non hai unha metodoloxía concisa. Resúmese na necesidade de adaptarse aos cambios. Prioriza:

1. As persoas e as interaccións sobmre os procesos e ferramentas.
2. O software que funciona sobre a documentación exhaustiva.
3. A colaboración co cliente sobre o contrato.
4. Responder ante o cambio sobre o seguemento do plan.

### 12 Principios

1. Satisfacer ao cliente
2. Abrazar o cambio
3. Entregar frecuentemente
4. Colaboración entre negoció e desenvolvemento
5. Individuos motivados
6. Comunicación cara a cara
7. Produto funcionando
8. Ritmo sostible
9. Excelencia
10. Simplicidade
11. Autoxestión
12. Reflexión e mellora

## 2. Testing e axilismo

- É clave na adaptación ao cambio
- Permite intergrar nun sistema de CI/CD
- Ritmo sostible
- Excelencia téncia e bo deseño

Estes son os puntos onde o testing é chave na rlación a prácticas de desenvolvemento áxiles.

## 3. Testing e CI/CD

Integra o código de equpos que traballan en paralelo soe ser problemático porque se producen conflitos.

A CI é unha práctia e proba o código frecuente e automaticamente.

Está basedo no control de versions, test automatizados e na automatización e un cambio cultural.

A entrega continua (CD) é a prácia que sonsiste en entregar que consiste en entregar versións de código o máis rápido posible.

Esta baseada nun desprege de premer un boónt e semiautomático. No se pode confundir entrega continua con despregue continuo.

## 4. Conceptos de TDD e ADTT

TDD. Test driven development ou desenvolvemento guiado por tests. Técnicas que consiste en traducir os casos de uso a exemplos concretos, convertidos en tests, que se escriben primeiro e logo se satisfacen no software e na refactorizacrión.

ATDD. Acceptance test driven development ou desenvolvemento guiado por tests de aceptación. Técnicas de desenvolvmento que consiste en definir os criterios de aceptación dunha historia de usuario xundo con negocio.

## 5. Tipos de tests

Depende co criterio que se use:

- Esteticos, dinámicos e pasivos.
- De caixa negra, branca e gris.
- Por alcance unitario, integración, sistema ou aceptación.
- UX / usabilidade, test A/B,
- Funcionais, non funcionais e de rendemendo

**Test de aceptación**: Definicións do que debe facer o sistema.
**Test unitario**: Proba una clase de xeito aillado (SUT). Piar básico en TDD.
**Test de integración** ou **de compoñente**. Proba a integración entre varias clases. Poden ter dependencias externas. Deben cubrir os mesmos principios que os unitarios.

## 6. Principios de testing

Deben ter calidade e ser relevantes para evitar que sexan contraproducentes.
Deben ser independentes da orde, da máquina, do SO, dos recursos e sistemas externos.
Deben autovalidarse automaticamente usarndo asercións.
Deben ser repetibles e inocuos. Cada execución sera o mesmo resultado e non xera cambios de estado.
Rápidos.
Descriptivos debe describir a funcionalidade e ter nome descriptivo.

## 7. Test unitarios

JUnit é un framework opensource para a automatización de teste en Java creadopor Erich Gramma e Kent Beck. Proporciona control sobre a execuión de probas e sobre as condicions de validacións.
Con JUnit 5 cada un dos tests unitarios dunha clase escríbese nunha clase espello co mesmo nome pero acabado en Test. Dentro dela temos unha estrutura de preparación de teste, execución e finalización. mediante anotacións @BeforeEach, @Test e @AfterEach.
