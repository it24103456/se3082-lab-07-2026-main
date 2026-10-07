# Builds and runs all six programs from Exercises 1-6.
# Usage:  make          build everything into ./bin
#         make run      run all six with 4 processes
#         make clean    remove ./bin
# If mpirun refuses to start (e.g. running as root, or fewer cores than
# processes), pass extra flags:  make run MPIRUN_FLAGS="--oversubscribe"

CC          = mpicc
CFLAGS      = -O2 -Wall
MPIRUN      = mpirun
MPIRUN_FLAGS =
NP          = 4

BIN = bin
PROGS = sum_bcast sum_scatter sum_gather sum_reduce sum_allreduce sum_scan

all: $(addprefix $(BIN)/,$(PROGS))

$(BIN):
	mkdir -p $(BIN)

$(BIN)/sum_bcast: ../Exercise01/sum_bcast.c | $(BIN)
	$(CC) $(CFLAGS) -o $@ $<

$(BIN)/sum_scatter: ../Exercise02/sum_scatter.c | $(BIN)
	$(CC) $(CFLAGS) -o $@ $<

$(BIN)/sum_gather: ../Exercise03/sum_gather.c | $(BIN)
	$(CC) $(CFLAGS) -o $@ $<

$(BIN)/sum_reduce: ../Exercise04/sum_reduce.c | $(BIN)
	$(CC) $(CFLAGS) -o $@ $<

$(BIN)/sum_allreduce: ../Exercise05/sum_allreduce.c | $(BIN)
	$(CC) $(CFLAGS) -o $@ $<

$(BIN)/sum_scan: ../Exercise06/sum_scan.c | $(BIN)
	$(CC) $(CFLAGS) -o $@ $<

run: all
	@for p in $(PROGS); do \
		echo "=== $$p (np=$(NP)) ==="; \
		$(MPIRUN) $(MPIRUN_FLAGS) -np $(NP) $(BIN)/$$p || exit 1; \
		echo; \
	done

clean:
	rm -rf $(BIN)

.PHONY: all run clean
