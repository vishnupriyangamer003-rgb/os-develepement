# OS Development — MiniOS + BotOS

Monorepo for OS-level experiments spanning bare-metal and application-level systems.

- **MiniOS** (`basic os develepement/`): Educational x86-64 monolithic OS built from scratch (Multiboot2 + GRUB, freestanding C + NASM, QEMU). Boots from bare metal to shell, virtual memory, and preemptive multitasking.
- **BotOS** (`basic os develepement/botos/`): Personal AI Operating System in PHP 8.2 — the Body & Action Controller for Atom AI (workspace tools, web research, task orchestration, two-tier human approval, Tri-Engine Command Center).

## 📁 Repository Layout

```
.
├── basic os develepement/   # MiniOS root
│   ├── arch/x86_64/         # GDT/IDT, paging, CPU init
│   ├── boot/                # GRUB cfg, linker script
│   ├── kernel/              # Kernel core + include/
│   ├── drivers/             # VGA, Serial, Keyboard, Timer
│   ├── lib/                 # Freestanding C library
│   ├── build/               # Ephemeral .o / .elf / .iso (git-ignored)
│   ├── scripts/             # Toolchain checks, build automation
│   ├── tests/               # QEMU unit/integration tests
│   ├── docs/                # architecture.md, build-guide.md, development-roadmap.md, decisions.md
│   ├── botos/               # BotOS app (PHP 8.2 + web UI + mobile worker)
│   ├── Makefile             # kernel / iso / run / clean targets
│   └── README.md            # MiniOS full overview
└── README.md                # This file
```

## 🚀 Quick Start

### 1. MiniOS (bare-metal, QEMU)

```bash
cd "basic os develepement"
make check-tools   # gcc, nasm, ld, grub-mkrescue, qemu-system-x86_64
make kernel        # Phase 2: build build/kernel.elf
make iso           # Phase 2: build build/minios.iso
make run           # Phase 3+: boot in QEMU
```

See: [`basic os develepement/docs/build-guide.md`](<basic os develepement/docs/build-guide.md>)

### 2. BotOS (PHP 8.2 + XAMPP)

```powershell
Copy-Item "basic os develepement\botos\.env.example" "basic os develepement\botos\.env"
& "d:\xampp\php\php.exe" -S localhost:8000 -t "basic os develepement\botos\public"
# open http://localhost:8000
```

See: [`basic os develepement/botos/README.md`](<basic os develepement/botos/README.md>)

## 🗺️ Status

- **MiniOS Phase 1:** Architecture & Environment — Completed (Day 1). Phases 2–10 (bootable ISO → shell → memory → multitasking → tests) planned.
- **BotOS Phase 1:** Architecture & Planning (Dual-Machine + Tri-Engine, ADR 001–010) — Completed (Day 1). Phases 2–10 (runtime → UI → RAG → devices → orchestration) planned.

## 🛡️ Principles

1. **Host isolation:** MiniOS only runs in QEMU; never touches host disks/bootloader.
2. **Freestanding:** MiniOS uses `-ffreestanding -nostdlib`, no host libc.
3. **Artifact isolation:** `build/`, `*.elf`, `*.iso`, `.env`, `vendor/` are git-ignored.
4. **Human approval:** BotOS state-changing actions require explicit UI approval.

## 📚 Docs

- MiniOS: [Overview](<basic os develepement/README.md>) · [Architecture](<basic os develepement/docs/architecture.md>) · [Roadmap](<basic os develepement/docs/development-roadmap.md>) · [Build Guide](<basic os develepement/docs/build-guide.md>) · [Decisions](<basic os develepement/docs/decisions.md>)
- BotOS: [Overview](<basic os develepement/botos/README.md>) · [Architecture](<basic os develepement/botos/docs/architecture.md>) · [API Design](<basic os develepement/botos/docs/api-design.md>) · [Security](<basic os develepement/botos/docs/security.md>) · [Device Integration](<basic os develepement/botos/docs/device-integration.md>)

## 🧰 Requirements

- MiniOS: `gcc`, `nasm`, `ld`, `grub-mkrescue`, `qemu-system-x86_64`, GNU Make
- BotOS: Windows 11 + XAMPP (PHP 8.2), optional Samsung Galaxy M31 worker over LAN

