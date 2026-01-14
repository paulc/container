
FROM dev-base

RUN rustup toolchain add nightly
RUN rustup default nightly
RUN rustup target add --toolchain nightly riscv32imc-unknown-none-elf riscv32imac-unknown-none-elf 
RUN rustup target add --toolchain nightly riscv32imc-unknown-none-elf riscv32imac-unknown-none-elf 
RUN rustup component add --toolchain nightly rust-analyzer rust-src llvm-tools

