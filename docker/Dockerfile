FROM ubuntu:24.04

RUN groupadd -r appuser && \
    useradd -r -g appuser -d /app -s /sbin/nologin appuser

RUN apt-get update && \
    apt-get upgrade -y --no-install-recommends && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        python3 \
        qemu-user-static \
        git \
        gcc \
        make \
        build-essential \
        gdb-multiarch \
        qemu-system-misc \
        gcc-riscv64-linux-gnu \
        binutils-riscv64-linux-gnu \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY --chown=appuser:appuser scripts /app/scripts

RUN find /app/scripts -type f -exec chmod +wr {} + && \
    chmod 755 /app/scripts/run.sh && \
    chown -R appuser:appuser /app
  #chmod 755 директория — предоставить владельцу полные права -rwxr-xr-x, а остальным пользователям право только на чтение и выполнение.chmod 644 директория — предоставить права на чтение и запись для владельца каталога, а остальным пользователям и группам оставить только на чтение содержимого.#644
USER appuser

ENTRYPOINT ["/app/scripts/run.sh"]

