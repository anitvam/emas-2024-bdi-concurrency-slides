+++
title = "On the external concurrency of current BDI frameworks for MAS"
outputs = ["Reveal"]
+++

# On the external concurrency 
# of current BDI frameworks for MAS

<br>

Martina Baiardi, Samuele Burattini, Giovanni Ciatto <br />
Danilo Pianini, **Alessandro Ricci**, and Andrea Omicini

<small>Department of Computer Science and Engineering (DISI)<br>
Alma Mater Studiorum — Università di Bologna <br>
Via dell’Università 50, 47522 Cesena (FC), Italy </small>

---

## BDI Agents

Architettura BDI -> mettiamo il puntino su qual è l'architettura di riferimento

Noi, a partire da questo, abbiamo fatto un nostro formalismo per descrivere la concorrenza,

---

## Computational Autonomy
<br>

- **Computational autonomy** is a pre-requisite for **autonomy** in software agents
- Agent's control-flow &rarr; mainstream programming languages concurrency abstractions <br> (e.g., thread, process, ...) 


---

## Which concurrency abstraction is the most appropriate?

- The selection of an appropriate concurrency model deeply impacts several aspects of the agent programming framework 
  - The **efficiency** of the MAS may improve, but
  - **predictability** and **reproducibility** may be affected.
- **Capturing and controlling concurrency is crucial, <br />and they often are hidden under the framework abstractions** 


---

## Which concurrency?

We distinguish between **internal** and **external** concurrency

{{% multicol %}}
{{% col %}} 

<div class="text-center">

### Internal Concurrency

\begin{aligned}
Agent ::== Perceive \parallel Deliberate \parallel Act
\end{aligned}

\begin{aligned}
Perceive ::== (\verb|perceive|_1 \parallel \ldots \parallel \verb|perceive|_M) \cdot Sense
\end{aligned}

\begin{aligned}
Deliberate ::== (Deliberate_1 \parallel \ldots \parallel Deliberate_L) \cdot Deliberate
\end{aligned}

\begin{aligned}
Act ::== (Act_1 \parallel \ldots \parallel Act_K) \cdot Act
\end{aligned}

</div>

{{% /col %}}
{{% col %}} 

<div class="text-center">

### External Concurrency

\begin{aligned}
Mas ::== Agent_1 \parallel \ldots \parallel Agent_N 
\end{aligned}

\begin{aligned}
Agent ::== \verb|sense| \cdot \verb|deliberate| \cdot \verb|act| \cdot Agent \\
\end{aligned}

</div>

{{% /col %}}
{{% /multicol %}}

---

## External Concurrency
#### Which concurrency abstraction are considered to map Agents' execution?

- **Threads**
- **Processes**
- **Event Loops**
- **Executors**

---

## Common concurrency patterns for MAS

- **One-Agent-One-Thread** ( **1A1T** )
- **All-Agents-One-Thread** ( **AA1T** )
- **All-Agents-One-Event-Loop** ( **AA1EL** )
- **All-Agents-One-Executor** ( **1A1E** )
  - With a **fixed**-size thread pool
  - With a **variable**-size thread pool 

---

## Analysis on BDI frameworks:


{{% multicol %}}
{{% col %}} 

<div class="text-center">

### Methodology

We inspected external concurrency in three steps:

1. **Empirical Evaluation** through a synthetic benchmark
2. **Documentation** and **source code inspection** of the selected BDI frameworks
3. **Direct contact** with maintainers

</div>

{{% /col %}}
{{% col %}} 

<div class="text-center">

### Framework selection

We selected actively-maintained and open source BDI programming frameworks:
- **Astra**
- **GOAL**
- **Jadex**
- **JaKtA**
- **Jason**
- **PHIDIAS**
- **SPADE-BDI**

</div>

{{% /col %}}
{{% /multicol %}}

---

## Benchmark

{{% multicol %}}
{{% col %}} 

<div class="text-center">

### Agent: PINGER

```text
!ping.
+!ping <- 
    .revealCurrentThread("intention 1");
    .send(pong, tell, ball);
    !!showThread(2);
    .revealCurrentThread("intention 1").
+ball <-
    !!showThread(4);
    .revealCurrentThread("intention 3").
+!showThread(X) <- .revealCurrentThread("intention " + X).
```

</div>

{{% /col %}}
{{% col %}} 

<div class="text-center">

### Agent: PONGER

```text
+ball[source(X)] <-
    .revealCurrentThread("intention 5");
    .send(X, tell, ball);
    !!showThread(6);
    .revealCurrentThread("intention 5").
+!showThread(X) <- .revealCurrentThread("intention " + X).
```

</div>

{{% /col %}}
{{% /multicol %}}

---

## Results

<img src="images/image.png" />
 
---