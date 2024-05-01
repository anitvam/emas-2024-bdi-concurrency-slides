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
Agent ::== Sense \parallel Deliberate \parallel Act
\end{aligned}

\begin{aligned}
Sense ::== (Sense_1 \parallel \ldots \parallel Sense_M) \cdot Sense
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
