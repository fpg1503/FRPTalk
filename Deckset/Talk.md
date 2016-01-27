# [fit] *FRP* em **Swift**
## [fit] by **Francesco Perrotti-Garcia**

---

![left](gravatar.jpg)

# [fit] *Francesco* 
# [fit] *Perrotti-Garcia*
# [fit] iOS Developer
# [fit] **_@fpg1503_**
# [fit] *PlayKids* - Movile

---

![](movile.jpg)

---

![fit](playkids.png)


--- 

# [fit] Functional reactive programming
# [fit] is a programming paradigm for 
# [fit] **_reactive programming_**
# [fit] using the building blocks of 
# [fit] **_functional programming._** 

---

# Functional Programming
- State
- Side Effects
- Functions

---

#[fit] State

---

![](state.gif)


---

# [fit]Side Effects

---

#[fit]Functions

---

# [fit] Reativo

---

# Reage a mudanças

---

![](domino.gif)

---

#[fit] FRP

- Declarativo

^ [...] this form must be declarative ("what to be") rather than imperative ("how to do").

- Composição

^ "Composition" is the principle of putting together simpler things to make more complex things, then putting these together to make even more complex things, and so on. This "building block" principle is crucial for making even moderately complicated constructions; without it, the complexity quickly becomes unmanageable.

---
# [fit]RAC

- Streams de eventos

---

```swift
let searchStrings = textField.rac_textSignal()
    .toSignalProducer()
    .map { text in text as! String }
```

---


# Evento

- `Event`
- Formaliza _algo aconteceu_
- Enviado por um Signal
- Recebido por Observer

---

# [fit]Enum

---

![fit](chris.gif)


---

# [fit] `Next`

^  event provides a new value from the source.

---

# [fit] `Failed`

^ event indicates that an error occurred before the signal could

---


# [fit] `Completed`

---

# [fit] `Interrupted`

^ event indicates that the signal has terminated due to
   cancellation, meaning that the operation was neither successful nor
   unsuccessful.

---

```swift
let searchResults = searchStrings
    .flatMap(.Latest) { (query: String) -> SignalProducer<(NSData, NSURLResponse), NSError> in
        let URLRequest = self.searchRequestWithEscapedQuery(query)
        return NSURLSession.sharedSession().rac_dataWithRequest(URLRequest)
    }
    .map { (data, URLResponse) -> String in
        let string = String(data: data, encoding: NSUTF8StringEncoding)!
        return self.parseJSONResultsFromString(string)
    }
    .observeOn(UIScheduler())
```


---

# [fit] Hot e Cold

---

# [fit] `SignalProducer`
- Cria `Signal`
- "Performa" efeito colateral

---

# [fit] Erros

--- 

# [fit] `throws`

---

# [fit] Blocos??

---

# [fit] 😔

---

# [fit] `returnValue: AnyObject?, error: ErrorType`

---

# [fit] Resposta e não erro 😬

---

# [fit] Não resposta e erro 🙃

---

# [fit] Não esposta e não erro 😐

---

# [fit] Resposta e erro 🤔

---

# [fit] `SignalProducer<AnyObject?, Error>`

---

# [fit] `SignalProducer<AnyObject?, NoError>`


---

#[fit] Properties

---

# [fit] `PropertyType`
## Bind usando `<~`
### `MutablePropertyType`

---

#[fit] `property <~ signal`

^  a [signal](#signals) to the property, updating the
  property’s value to the latest value sent by the signal.

---

#[fit] `property <~ producer` 

^ starts the given [signal producer](#signal-producers),
  and binds the property’s value to the latest value sent on the started signal.

---

#[fit] `property <~ otherProperty`

^ binds one property to another, so that the destination
  property’s value is updated whenever the source property is updated.

---

# [fit] `DynamicProperty`

## KVC ou KVO

---

#[fit] `MutableProperty` >> `DynamicProperty`


---

#[fit] Rx

---

#[fit] Rx
 * Inspiração grande
 * API mais simples
 * Endereçar confusões comuns
 * Mais próximo do Cocoa

---

# [fit] RAC vs Rx

---

# [fit] Uso

- Simples mais difícil
- Novo paradigma
- Intelegibilidade do código

---

# [fit] Demo

---

![](timcook.gif)

---

# [fit] *Quando* não *usar*

- Times grandes
- Time heterogêneo
- Outros riscos

---

![fit](rac.gif)

---

![fit](rac2.gif)

---

# [fit] Como começar então?

- Validação de forms
- Partes isoladas
- Projetos pessoais

---

# [fit] Alternativas

## Futures

---

![fit](paulinho.gif)

---

#[fit] Referências

---

# Code

- [Elm]
- [RX]
- [RAC]
- [Delta]
- [Future]
- [Swift-Flow]
- [ReduxKit]
- [Moya]

---

# Talks

- [Back to the Futures](https://realm.io/news/swift-summit-javier-soto-futures)
- [Beyond the block based API: Building a simple Future](https://github.com/Thomvis/SFSwiftSummit2015)


---

# SO

- [What is FRP](http://stackoverflow.com/a/1030631/2305521)
- [RAC vs RxSwift](http://stackoverflow.com/a/32581824/2305521)

---

# State

- 📄 [Local State is Poison](https://awelonblue.wordpress.com/2012/10/21/local-state-is-poison/)

---

# Monads

- 🎞 [Don't fear the Monad](https://www.youtube.com/watch?v=ZhuHCtR3xq8)
- 📄 [Monads are elephants](http://james-iry.blogspot.com.br/2007/09/monads-are-elephants-part-1.html) 
	- [Part 2](http://james-iry.blogspot.com.br/2007/10/monads-are-elephants-part-2.html)
	- [Part 3](http://james-iry.blogspot.com.br/2007/10/monads-are-elephants-part-3.html)
	- [Part 4](http://james-iry.blogspot.com.br/2007/11/monads-are-elephants-part-4.html)

---

# [fit] Q&A

---

# [fit] Obrigado! 