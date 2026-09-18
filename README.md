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



