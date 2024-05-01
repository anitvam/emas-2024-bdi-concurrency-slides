+++
title = "JaKtA"
outputs = ["Reveal"]
+++

# JaKtA: BDI agent-oriented programming in pure Kotlin

<br>


Martina Baiardi, Samuele Burattini, Giovanni Ciatto, and Danilo Pianini

<small>Department of Computer Science and Engineering (DISI)<br>
Alma Mater Studiorum — Università di Bologna <br>
Via dell’Università 50, 47522 Cesena (FC), Italy </small>

---

{{% section %}}

## Current trend: multi-paradigm languages
<br>

Several languages include more than one paradigm:


| Language | Object-Oriented | Functional |
| :---:  | :---: | :---: |
| Java  | {{< tick >}} {{< /tick >}} | {{< maybe >}} (Java 8){{< /maybe >}} |
| C#    | {{< tick >}} {{< /tick >}} | {{< maybe >}} {{< /maybe >}} |
| Scala | {{< tick >}} {{< /tick >}} | {{< tick >}} {{< /tick >}} |
| Kotlin| {{< tick >}} {{< /tick >}} | {{< tick >}} {{< /tick >}} |
| Ruby  | {{< tick >}} {{< /tick >}} | {{< maybe >}} {{< /maybe >}} |
| Caml | {{< maybe >}} (OCaml) {{< /maybe >}} | {{< tick >}} {{< /tick >}} |
| Python | {{< tick >}} {{< /tick >}} | {{< maybe >}} {{< /maybe >}} |
| JavaScript| {{< maybe >}} {{< /maybe >}} | {{< maybe >}} {{< /maybe >}} |

---

However, Agent-Orientation / BDI is never considered

| Language | Object-Oriented | Functional | Agent-Oriented
| :---:  | :---: | :---: | :---: |
| Java  | {{< tick >}} {{< /tick >}} | {{< maybe >}} (Java 8){{< /maybe >}} | {{< cross >}} {{< /cross >}} |
| C#    | {{< tick >}} {{< /tick >}} | {{< maybe >}} {{< /maybe >}} | {{< cross >}} {{< /cross >}} |
| Scala | {{< tick >}} {{< /tick >}} | {{< tick >}} {{< /tick >}} | {{< cross >}} {{< /cross >}} |
| Kotlin| {{< tick >}} {{< /tick >}} | {{< tick >}} {{< /tick >}} | {{< cross >}} {{< /cross >}} |
| Ruby  | {{< tick >}} {{< /tick >}} | {{< tick >}} {{< /tick >}} | {{< cross >}} {{< /cross >}} |
| Caml | {{< tick >}} (OCaml) {{< /tick >}} | {{< tick >}} {{< /tick >}} | {{< cross >}} {{< /cross >}} |
| Python | {{< tick >}} {{< /tick >}} | {{< maybe >}} {{< /maybe >}} | {{< cross >}} {{< /cross >}} |
| JavaScript| {{< maybe >}} {{< /maybe >}} | {{< maybe >}} {{< /maybe >}} | {{< cross >}} {{< /cross >}} |
{{% /section %}}


---

#### No *active* proposals for including *AOP/BDI abstractions* into mainstream languages
<br>

# WHY?

---

# BDI Libraries

<br>
<br>

{{% multicol %}} {{< col class="col-75">}}

* Built for mainstream languages
* Subject to the **syntactic restrictions** of their host language
  * "True" AOP/BDI feeling hardly achieved

{{< /col >}}

{{< col class="col-25">}}

{{< fragment >}}
## <i class="fa-solid fa-arrow-right"></i> **custom language**
{{< /fragment >}}

{{< /col >}} {{% /multicol %}}

---

# AOP Custom Languages
* <span class="green">Great ergonomy for BDI AOP (made by purpose) </span>
* <span class="red">BDI-specific, not multi-paradigm </span>
* <span class="red">Steep learning curve</span>
* <span class="red">Require custom tooling (IDEs, code suggestions, syntax highlighters, linters...)</span>
* <span class="red">Small community</span>
* <span class="red">High maintenance cost!</span>

---

# A hybrid approach

<!-- ![](images/ergonomy.png) -->

{{< figure src="images/ergonomy.png" width="60%" >}}

---

# JaKtA: <br> <u>Ja</u>son-like <u>K</u>o<u>t</u>lin <u>A</u>gents

Internal Domain-Specific Language (DSL) implemented in Kotlin

* Multi-paradigm support: OOP + FP + BDI AOP
* Hosted on a mainstream language: gentle learning curve
  * Great learning resources for Kotlin
  * Significantly large community for help
* Reuses the entire existing Kotlin toolchain
  * Developed and *maintained* by the language maintainers and the community
  * Maintenance is greatly reduced
* Good ergonomy

---

# Why kotlin?
<br>

{{% multicol %}}{{% col %}}
* Natively multi-paradigm (OOP + FP)
* Statically typed
  * With a good IDE, helps understanding what can be written where
* Direct support to internal DSLs
  * a.k.a "Type-safe builders" in the Kotlin documentation
* Support for multiplatform development
{{% /col %}}

{{< col class="text-center">}}

* Growing community
  * Strongly pushed by Google for Android
{{< figure src="images/android-kotlin.png" width="70%" >}}

{{% /col %}}{{% /multicol %}}


---
# Jakta architecture

{{< figure src="images/jacop_modules.svg" width="50%" >}}

---

## Jakta: multi-paradigm AOP/BDI+OOP+FP


```kotlin
mas {                                                   // BDI specification
  fun allPlayers(team: String) =
    Regex("""<a\s(\X*?)\sdata-cy="player">(.*)<\/a>""") // Object-oriented regex library
        .findAll(URL("https://www.besoccer.com/team/squad/$team").readText())
        .map { team to it.groupValues[2] }              // Lambda expression (Functional style)

  listOf("napoli", "milan", "internazionale")           // Kotlin standard library
      .flatMap(::allPlayers)                            // Higher-order function (Functional style)
      .forEach { (team, player) ->                      // Destructuring declaration
          agent(player) {
              beliefs { fact { squad(team) } }
              goals { achieve(start) }
              plans {
                  +achieve(start) onlyIf { squad(S).fromSelf } then {
                      execute(print("Hello! I play for", S))
                  }
              }
          }
      }
}.start()
```

<i class="fa-solid fa-file-code"></i> [SoccerMas.kt](https://github.com/jakta-bdi/jakta-examples/blob/main/src/main/kotlin/it/unibo/jakta/agents/examples/soccer/SoccerMas.kt)

---

# JakTa
<br>

(currently) JVM based with native Android support, mobile-ready

{{< figure src="images/android-tictactoe.png" width="50%" >}}


<i class="fa-solid fa-file-code"></i> [TicTacToeMas.kt](https://github.com/jakta-bdi/jakta-examples/blob/main/src/main/kotlin/it/unibo/jakta/agents/examples/tris/TicTacToeMas.kt)

<i class="fa-brands fa-android"></i> [Android Project](https://github.com/jakta-bdi/jakta-android-example)

---

# Future work

* {{% multicol %}}{{% col class="col-4" %}}
**Multiplatform targeting**
{{% /col %}}{{% col class="col-8"%}}
{{< figure src="images/jakta-mp.png" >}}
{{% /col %}}{{% /multicol %}}
* **Pluggable concurrency model**, neatly searating BDI definitions and the underlying threading
* **Improved DSL syntax** to further improve the multi-paradigm integration (AOP/BDI + OOP + FP)

---

# try jakta
<br>

[github.com/jakta-bdi/jakta-examples](https://github.com/jakta-bdi/jakta-examples)

{{< figure src="images/qr-code.svg" width="20%" >}}