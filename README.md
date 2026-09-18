Yes. GEM (Graphics Environment Manager) is particularly interesting because it sits between the world of DOS and what we would later call a modern desktop.

1. Who created GEM?

GEM was developed by Digital Research (DRI)—the company best known for CP/M—and was released on February 28, 1985.

It wasn't the invention of a single person. DRI developed it based on earlier graphics technology called GSX. One of the key figures in its early development was Lee Jay Lorenzen, who had experience working at Xerox PARC.

And there is an important distinction to be made here:

> GEM originated at Digital Research for PCs, but it became especially well-known through the Atari ST.

Atari began working with DRI to adapt GEM for the Motorola 68000 processor in September 1984, and GEM became the graphical interface for the Atari ST's TOS (Tramiel Operating System) in 1985.

---

2. What was the "layer" structure of GEM?

On the PC, you can visualize it roughly like this:

┌─────────────────────────────┐
│       GEM Application       │
│   DTP / drawing / editor    │
├─────────────────────────────┤
│            AES              │
│  windows, events, menus     │
├─────────────────────────────┤
│            VDI              │
│   graphics, text, drawing   │
├─────────────────────────────┤
│           GEMDOS            │
│ files / memory / DOS        │
├─────────────────────────────┤
│           MS-DOS            │
├─────────────────────────────┤
│          Hardware           │
└─────────────────────────────┘

On the Atari ST, the structure was conceptually similar, but TOS bundled the system components together, including GEM and GEMDOS.

The two components most relevant to your question are:

AES — Application Environment Services

This was the part responsible for the interface and the management of applications and windows.

It handled things like:

windows;

menus;

events;

mouse;

keyboard;

interface objects;

inter-application communication.


VDI — Virtual Device Interface

This was the graphics layer.  For example, an application could request:

"draw a line"
"write this text"
"fill this rectangle"

without needing to know all the details of the graphics hardware.


---

3. How did the window manager work?

GEM relied on a very important concept: the application did not need to directly control the entire screen.

Imagine two applications:

┌──────────────────────────────────┐
│ GEM Desktop                      │
│                                  │
│ ┌──────────────┐ ┌─────────────┐ │
│ │ Program A    │ │ Program B   │ │
│ │              │ │             │ │
│ │              │ │             │ │
│ └──────────────┘ └─────────────┘ │
│                                  │
└──────────────────────────────────┘

The manager knew:

which window was on top;

which one had the focus;

which part of the window was visible;

which part was hidden by another window.


When a window was revealed, the system could ask the application to redraw the newly visible section.


---


4. How did program switching work?

Here, one must be careful to note a historical difference.

GEM did not operate like modern Windows NT or Windows, where each application runs in a protected process and the kernel can interrupt it at any moment.

In the classic GEM environment—especially on the Atari ST—execution was essentially cooperative.

We can visualize it like this:

GEM
                  │
        ┌─────────┴─────────┐
        │                   │
        ▼                   ▼
    Program A           Program B
        │                   │
        └──── yields ───────┘
             control

Switching applications depended on how the environment and the applications cooperated.

Therefore:

switching windows ≠ necessarily switching processes, as in modern Windows.


---

5. What about memory?

This is where there is a huge difference between GEM/Atari ST and modern Windows.

The Atari ST's Motorola 68000 processor had a much larger address space than the 8086, and TOS used a linear memory model.

For example, on an ST with 512 KB:

Memory
000000 ┌──────────────────┐
       │ TOS / system     │
       ├──────────────────┤
       │ GEM              │
       ├──────────────────┤
       │ Desktop          │
       ├──────────────────┤
       │ application      │
       ├──────────────────┤
       │ data / heap      │
       ├──────────────────┤
       │ other application│
       └──────────────────┘

This representation is conceptual; it does not mean that every ST had exactly this layout.

The key point is that you didn't have the modern model:

Program A → isolated virtual space
Program B → isolated virtual space

with full memory protection.

This meant that a poorly behaved program could cause problems for the system or for other applications.


---

6. GEM on the Atari ST was even more interesting

For the Atari ST, Atari adapted GEM for the Motorola 68000.

Development of this version began in 1984, when Atari engineers went to work with Digital Research.  Initially, the plan was to use CP/M-68K, but Atari ultimately used GEMDOS—a DOS-like layer—and named the complete system TOS (The Operating System).

The structure looked roughly like this:

APPLICATION
                 │
        ┌────────┴────────┐
        │                 │
       AES               VDI
        │                 │
        └────────┬────────┘
                 │
              GEMDOS
                 │
                 ▼
                TOS
                 │
                 ▼
            Motorola 68000

This explains why the Atari ST could boot into a graphical environment so quickly: in later ST models, TOS was actually stored in ROM.


---

7. So, where did it first appear?

There are two answers that need to be distinguished:

GEM as a product: it originated at Digital Research and was released in February 1985.

GEM as a particularly famous commercial computing platform: it appeared on the Atari ST (released in 1985), where it became the graphical interface for TOS.

In other words:

Digital Research
       │
       │ develops GEM
       ▼
     GEM
       │
       ├──── PC / MS-DOS
       │
       └──── Atari
               │
               ▼
             TOS
               │
               ▼
           Atari ST

And there is an interesting historical footnote: GEM was influenced by the graphical tradition of Xerox PARC and ended up looking enough like the Macintosh for Apple to challenge certain aspects of its "look and feel"; this led to changes in the PC versions.

If you want to understand it at the memory level, the next interesting step is to take apart an Atari ST.


