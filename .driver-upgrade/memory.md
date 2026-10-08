# psycopg2 driver upgrade memory

## Build and test commands

- Build: `python3.12 setup.py build`
- Build location: `build/lib.3.12/psycopg2/`
- Traditional tests: `PYTHONPATH=build/lib.3.12 python3.12 -c "import tests; tests.unittest.main(defaultTest='tests.test_suite')" --verbose`
- Install for testing: `pip install -e .` (required before running pytest)

## Learned this run

- The yugabyte tests (test_fallback_topology.py, test_rr1.py, test_rr2.py) require the package to be installed before pytest can collect them. Running `pip install -e .` installs the package in editable mode, which allows pytest to import psycopg2 and its modules.
- The editable install creates a .so file in lib/ that should be removed to keep the worktree clean: `lib/_psycopg.cpython-312-x86_64-linux-gnu.so`
- The core dump file `core.2087` was left behind and needed to be removed.
