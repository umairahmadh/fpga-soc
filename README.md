# 05 · SoC Integration

**Part of [FPGA Journey](https://github.com/YOUR_USERNAME/fpga-journey)**

> Connecting a CPU to the real world: bus fabric, memory map, peripherals, and running C programs on a computer you built yourself.

The moment your own RISC-V core executes a `printf("Hello from my CPU!\n")` over a UART you also designed is the moment the whole stack becomes real.

---

## 🎯 Learning Objectives

- Bus architectures: Wishbone and AXI-Lite — address decoding, arbitration, wait states
- Memory-mapped I/O: how a CPU "talks to" peripherals via loads and stores
- Linker scripts and startup code: what happens before `main()`
- LiteX: a Python SoC builder that lets one person assemble a full system fast
- Running compiled C programs on bare-metal hardware you designed

---

## 📁 Structure

```
fpga-05-soc/
├── docs/
│   ├── memory_map.md           # Address space: BRAM, UART, timer, GPIO
│   ├── bus_architecture.png    # Block diagram: CPU ↔ bus ↔ peripherals
│   └── boot_sequence.md        # What happens from reset to main()
├── 01_wishbone/
│   ├── rtl/
│   │   ├── wb_bus.sv           # Simple single-master Wishbone B4 fabric
│   │   ├── wb_bram.sv          # Wishbone-attached block RAM
│   │   ├── wb_uart.sv          # UART with Wishbone interface
│   │   └── wb_gpio.sv          # GPIO with Wishbone interface
│   ├── tb/
│   │   └── wb_bus_tb.sv        # Bus transactions + address decoding test
│   └── README.md
├── 02_custom_soc/
│   ├── rtl/
│   │   └── soc_top.sv          # Your RV32I core + Wishbone bus + peripherals
│   ├── sw/
│   │   ├── startup.s           # Reset vector, stack setup
│   │   ├── link.ld             # Linker script (BRAM memory layout)
│   │   ├── uart.c / uart.h     # UART driver (memory-mapped)
│   │   ├── hello.c             # Your first bare-metal C program
│   │   └── Makefile            # riscv-gcc → .elf → .hex → load into sim
│   ├── tb/
│   │   └── soc_tb.sv           # Load hex, run, check UART output
│   └── README.md
├── 03_litex/
│   ├── target_sim.py           # LiteX SoC for simulation (no hardware needed)
│   ├── target_arty.py          # LiteX SoC targeting Arty A7 (if you have one)
│   ├── sw/
│   │   └── demo.c              # C demo using LiteX-generated CSR headers
│   └── README.md               # LiteX workflow: generate → build → run
└── Makefile
```

---

## ✅ Project Checklist

**Bus & memory**
- [ ] Wishbone bus fabric — address decoding, correct ACK timing
- [ ] Wishbone BRAM slave — read/write, wait states
- [ ] Wishbone UART slave — TX/RX registers, status bits

**Custom SoC**
- [ ] RV32I core (from repo 04) connected to Wishbone bus
- [ ] Linker script and startup assembly written and understood
- [ ] Bare-metal C: blinks a simulated LED via GPIO
- [ ] Bare-metal C: prints "Hello, world!" over UART
- [ ] SoC runs a Fibonacci sequence program, output verified

**LiteX**
- [ ] LiteX simulation target builds and runs
- [ ] Demo C program runs on LiteX SoC
- [ ] (Optional) LiteX design on real board with UART terminal output

---

## 💡 The Rewarding Moment

The first time your own CPU executes code that was compiled by GCC, linked with your linker script, and communicates through your UART peripheral — that's the full hardware-software stack. No black boxes.

When that works in simulation, you understand the machine. When it works on silicon, you've built one.

---

## 🛠️ Tools

| Tool | Purpose |
|------|---------|
| Verilator | Simulate the full SoC |
| LiteX | Python SoC builder (`pip install litex`) |
| riscv-gnu-toolchain | Compile bare-metal C |
| picocom / minicom | Terminal for UART output on real hardware |
| GTKWave | Debugging bus transactions |

---

## 📖 Resources

- [LiteX wiki](https://github.com/enjoy-digital/litex/wiki) — start here
- [Wishbone B4 spec](https://cdn.opencores.org/downloads/wbspec_b4.pdf)
- [Bare metal RISC-V from scratch](https://github.com/noteed/riscv-hello-c)
- [ZipCPU: Designing a bus](https://zipcpu.com/blog/2017/06/08/simple-wb-master.html)

---

**← Previous:** [04 · RISC-V CPU](https://github.com/YOUR_USERNAME/fpga-04-riscv-cpu) &nbsp;|&nbsp; **See also:** [06 · Verification](https://github.com/YOUR_USERNAME/fpga-06-verification) &nbsp;|&nbsp; **Next →** [07 · Research](https://github.com/YOUR_USERNAME/fpga-07-research)
