# Operating Systems — Kernel do Zero
#week 

## Objectivos
- Boot process: BIOS/UEFI → bootloader → kernel
- x86 protected mode, GDT, IDT
- Memory management: physical memory, virtual memory, paging
- Process scheduling: round-robin, CFS (Completely Fair Scheduler)
- Synchronization: spinlocks, mutexes, semaphores no kernel
- System calls: user mode → kernel mode transition

## Recursos

| Tipo   | Recurso                                                        |
| ------ | -------------------------------------------------------------- |
| Livro  | _Operating Systems: Three Easy Pieces_ — gratuito em ostep.org |
| Guide  | OSDev Wiki — wiki.osdev.org (a referência)                     |
| Código | xv6 — github.com/mit-pdos/xv6-riscv (kernel didáctico do MIT)  |
| Video  | "Writing an OS in Rust" — Philipp Oppermann (blog + YouTube)   |
| Sim    | QEMU — emulador gratuito para testar o kernel                  |

## Projeto
### Mini Kernel Bootável (x86 ou RISC-V via QEMU)

**Tech Stack:** C + Assembly (x86 ou RISC-V) + QEMU

**Overview**
	Um kernel operativo do zero que arranca via GRUB, tem um shell básico onde podes escrever comandos, e consegue fazer fork de processos simples — tudo emulado no QEMU sem necessitar de hardware. O boot process começa com o GRUB a carregar o kernel em modo protegido x86, inicializas a GDT (Global Descriptor Table) e IDT (Interrupt Descriptor Table) para gerir interrupts, e o primeiro output é "Hello from the kernel" via driver VGA básico. O memory manager usa um bitmap allocator para páginas físicas de 4KB e activa a paginação via page tables para isolamento de processos. O heap do kernel implementa `kmalloc` e `kfree` com um free list simples. O scheduler usa round-robin com fixed timeslice via timer interrupt (IRQ0). As syscalls básicas — `write` para output, `exit` para terminar um processo, e `fork` para duplicar um processo — ensinam a transição entre user mode e kernel mode via `int 0x80`. O shell lê do teclado via keyboard interrupt handler, parseia comandos simples, e executa programs em memória. Um in-memory filesystem (ramfs) permite "carregar" programas. Cada milestone tem testes automáticos via QEMU scripting

**Milestones obrigatórios:**

1. **Boot:** GRUB carrega o kernel, imprime "Hello Kernel" via VGA
2. **Interrupts:** IDT configurada, keyboard interrupt handler
3. **Memory:** physical memory manager (bitmap allocator), paging com 4KB pages
4. **Heap:** `kmalloc` e `kfree` simples
5. **Scheduling:** múltiplos processos com round-robin
6. **Syscalls:** `write`, `exit`, `fork` (básico)
7. **Shell:** lê comandos do teclado, executa programas simples
8. **Filesystem:** in-memory FS (ramfs) simples

**Processo de aprendizagem:**

- Cada milestone tem testes automáticos (via QEMU + scripts)
- Documenta cada decisão: "Porque GDT? O que é um segment descriptor?"

## Entregáveis

- [ ] Kernel bootável em QEMU (ISO)
- [ ] Blog: "Writing an OS From Scratch in C — Bootloader to Scheduler"
- [ ] Video: boot ao vivo no QEMU, com shell e fork a funcionar
- [ ] Documentação: diagrama de arquitectura do kernel

