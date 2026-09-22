# GCC DejaGnu `.exp` Practice

Learning exercises for GCC testsuite `.exp` files (DejaGnu / Tcl).

## Files
- `simple.exp` — demonstrates all result types: PASS, FAIL, XFAIL, XPASS, UNSUPPORTED, UNTESTED.
- `mypractice.exp` — a safe copy of `pr111527.exp` for experimenting.
- `compilecheck.exp` — actually runs the compiler: valid code compiles, invalid code is rejected, and error-message text is checked.
- `seefiles.exp` — like compilecheck but does NOT delete its temp files, to show where they are created on disk.

## How to run (inside a built GCC tree)
Copy an `.exp` into `gcc/testsuite/gcc.misc-tests/`, then from the build's `gcc` directory:

```bash
make check-gcc RUNTESTFLAGS="simple.exp"
```

Read results in:
- `testsuite/gcc/gcc.sum` — short summary (one line per test)
- `testsuite/gcc/gcc.log` — full detail (commands + output)

## Result-type model
"Expected vs unexpected" is about whether reality matched the prediction:

| Predicted | Actual | Reported | Alarming? |
|-----------|--------|----------|-----------|
| (nothing) | pass   | PASS     | no  |
| (nothing) | fail   | FAIL     | yes |
| failure (`setup_xfail`) | fail | XFAIL | no  |
| failure (`setup_xfail`) | pass | XPASS | yes |
