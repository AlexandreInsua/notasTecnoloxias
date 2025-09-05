_Felienne Hermans_

O que todo programador precisa saber sobre cognición.

# Prólogo de Jon Sheet

Staff Developer Relation Enginer en Google. A pesar de ter programado moito e axudado a moitos novatos nunca pensou sobre as relación enre programación e cognición. Ademáis, os seus coñecementos non son sistemáticos. O libro é unha contribución ao estudo da cuestion.

# Prefacio de Felienne Hermans

Profesora da Universidade de Leiden (Paises Baixos). Entender como funciona o cerebro cando programamos porque esta é unha actividade especialmente existente. Requiere un alto grando de atención e de abstracción onde se poden provocar moitos erros, moitos deles teñen a raíz en cuestións cognitivas. O propósito deste libro é axudar a entender como o cerebro procesa o código.

# Parte I. Como ler mellor código

## Decodificar a túa confusión mentres codificas

Ler un código pro primeiras ven ou reler un código propio poder ser confuso. Hai diferentes tipos de confusión relacionado con diferetnes tipos de procesos cognitivos.

### Diferentes tipos de confusión no código

Hai varios tipos de confusión

- Falta de coñecemento e remite á LTM (memoria a longo prazo)
- Falta de información e remita a STM (memoria a curto prazo)
- Falta de capacidade de procesamento. A dificultade de procesar moitos valores intermedios e acción ao mesmo tempo. Remite á WM (memoria de traballo).

### Diferentes procesos cognitivos que afectan á codificación

A falta de coñecemento está relacionado coa LTM, a falta de información está relacionado coa STM e falta de capacidade está relacionado coa WM.

### LTM e programación.

A memoria a longo prazo almacena diferente tipo de información (novos pensamentos)
A memoria a curto prazo.
A memoria de traballo.
Lendo código a LTM relaciónase co coñecemento da linguaxe (e do framework??), a STM co estado e a WM co seguemento e traza do código. Cando se precisa tomar notas para seguir a execución de código, a WM está saturada.

#### Speed reading for code

Ler código é a principal actividade do programador. Sobre o 60% do tempo, pero os programas docentes están centradas na producción de código e non na lectura crítica de código.
Hai factores que dificultan a lectura de código: saber o **que fai** o código, ter nomes de variables estrañas ou pouco habituais. Un código así limita a capacidade da STM. A STM funciona dentro de 30s e de 2 a 6 itens. Para facer frente estes límites colabora coa LTM.
Os experimentos de Gost sobre xadrez demostrou o poder de segmentación da información e agrupar segmentos para procesar e recordar conxuntos de información. Mesmo unha persoa intelixentes ten dificultade cando trata con estructura de conceptos de dominio que aínda non se gardan na LTM.

Cando se recibe un estímulo externo, antes de pasar á STM, a información é almacenada temporalmente nas memorias temporais chamadas sensorial. Para á vista temos a memoria icónica.
O importante non é que o que se recorda, senón como se lembra. Resulta fundamental fragmentar o código e para isto é útil usar patróns de código coñecidos. O código con comentarios necesita máis tempo para ser lido pero ser útil para fragmentar o código. Pódese usar comentarios para balizar temporalmente o código e facilitar a fragmentación, como titular as funcións. Outra formas de balizar é utilizar unha nómina adecuada.

### How to learn syntax quickly

Este capítulo ensina catro técnicas para memorizar conceptos de programación máis rápido e mellor.

#### Tips para lembrar a sintaxe

Hai que ter en conta que cando máis código se coñecer, mellor se fragciona. As interrupcións causan estragos no fluxo de traballo polo que consultar a documentción pode implicar unha interrupción grave.

- Usar flashcard. Aplicable a un código. A LTM funciona formando redes de conceptoss. Debido á curva de esquecemento tempos que recordar períodicametne o aprendido pero os estudos apúntan que é máis eficiente espacias as sesións
- Recordar a sintaxe + tempo. A LTM funciona de de dous xeitos: as forzas de almacenamento e de recuperación. A forza de almacenmento indica que algo está almacenado na LTM (como unha operación aritmética básica como 3 x 4 = 12). A forza de recuperación indica como é de doado de lembrar algo como a sintaxe de filter() cou reduce(). Cando tes algo na punta da língua está a fallar a forza de recuperación. A recuperación da información mellórase coa práctica, mesmo sen estudo especial, so recordando.
  Outra forma de reforzar a memoria de algo é reflexionar sobre isto, nun proceso coñecido como elaboración. Pódese usar esquemas. A elaboración implica que se adapta á nova info á información previa. Cando se aprende un novo concepto convén recorrer á elaboración para asentalo. Pódese seguir estas pistas.
- Relacionando con outros conceptos e xustificalos.
- Buscar alternativas no mesmo stack.
- Buscar equivalencias noutro stack.

#### Como ler código complexo

Enmárcase dentro da carga de procesamento. Hai situacións onde o código é demasiado complexo e sobrecarga a memoria de traballo. Mentres que a STM almacena información a WM procesaa. A WM tamén está limitada a media ducia de itens. Se tratas con máis elementos, supérase a carga cognitiva. Hai tres tipos de carga cognitiva.

- Carga intrínseca: aquela causada polas características dos problema en si, com a dificultades para calcular una hipótese.
- Carga externa: aquela causada polas distraccións externas ao problema, como se formula o problema e depende do grao de coñecemento previo e da familiaridade coa formulación.
- Carga relacionada: aquela creada por ter que gardar algo en LTM.

Técnicas para reducir a carga cognitiva:

- Refactorizar para mellorar a lexibilidade. Lexibilidade e mantenibilidade non é o mesmo. O naming é o punto de partida.
- Substituír os constructos poucos habituais na linguaxe. Por exemplo, usar programación imperativa en lugar de funcional.
- Usar código sinónimo para flashcards.

Axudas para a sobrecarda da memoria.

- Crear un gráfico de dependencias.
- Usar una tába de estados.
- Confirmar gráfico de dependencias e táboas de estado.

# Parte II. Pensar sobre o código

## Comprender mellor o código

### Tipos de variables

Desde un punto de vista funcional, considera variables de valor fixo, de paso (stepper), bandeiras, iterador(walker). valor actual, valor buscado, acumulador, contedor, seguidor/punteiro, organizadora e temporal.
Usa a Notación Húngara, prefixos cos tipos de variables.

### Obter mellor coñecemento dos programas

#### Niveis de coñecemento.

Texto e plan (profundo). O coñecemento do plan implcia saber que partes se relacionan entre si e como. A partir dun punto focal constrúen o seu coñedemento pasando á compresión local, de conceptos, da entidade e das múltiples entidades. O coñecemento textual é análogo ao idiomático, ao da linguaxe natural. Os programadores escanean o código despois de lolo. Os novatos fanno máis linearmente que os experimentados, que len seguindo a pilla de chamadas.

Estratexias que se oden aplicar á lctura de código.

- Activación de coñecemento previo.
- Monitoreo. Recomenda (ilexible) o código e anotalo (mellor comentalo)
- Visualización.
- Valorar a importancia das liñas.
- Inferir funcións do naming
- Facerlle preguntas ao código.
- Resumir código.

### Resovler mellor os problemas de programación

#### Usar modelos para pensar o código

Simplificar o probema e usar entidades
Modelo mental é unha abstracción que se pode usar para pensar sobre o problema en cuestión.
Axuda á memoria de traballo e funciona mellor canto máis específicos son:
máquina nocial

### Conceptos errados: erros no pensamento.

Asume que parte dos bugs son resultado de erros de pensamento.
Porque ler unha segunda linguaxe de programación e máis doada que a primeira. Porque se produce unha transferencia de coñecemento desde a primeira á segunda, sexa para aplicalo a conceptos coñecidos ou descoñecidos.
Esta transferencia pode ser consciente ou inconsciente e próxima ou afastada, positivo ou negativa, cando o coñecemento previo induce a erro no novo dominio.
O bugs soen ter como causa profunda una suposición errónea sobre o comportamento do código, por tanto, hai que liminar a concepción errada.

# Parte III. Escribindo mellor o código
