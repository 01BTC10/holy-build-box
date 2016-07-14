# Library variants

Holy Build Box provides several different variants of its static libraries, each compiled with different compilation flags and thus meant for different situations.

The static libraries in each variant are compiled with the flags as specified by its `STATICLIB_CFLAGS` environment variable.

## `exe`

This variant is meant for compiling applications. This is the variant that you have worked with so far in the [tutorials](README.md#tutorials).

### Caveats

This variant is not suitable for compiling shared libraries because the provided static libraries are not compiled with `-fPIC`. Use the `shlib` variant instead.

### Properties

 * `CFLAGS` and `CXXFLAGS`: `-g -O2 -fvisibility=hidden`
 * `LDFLAGS`: `-static-libstdc++`
 * `STATICLIB_CFLAGS` and `STATICLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden`
 * `SHLIB_CFLAGS` and `SHLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden`
 * `SHLIB_LDFLAGS`: `-static-libstdc++`
 * `O3_ALLOWED`: `true`
 * Activation command: `/hbb_exe/activate-exec`
 * Activation source script: `/hbb_exe/activate`


## `exe_gc_light_hardened`

This variant is is meant for compiling applications, but with dead-code elimination enabled and with a *small* amount of security hardening. This variant is especially suitable for compiling applications for use in production environments.

See [Security hardening binaries](SECURITY-HARDENING-BINARIES.md) for more information about the security flags.

The `exe_gc_hardened` variant is even better because it also enables full security hardening, but it has a number of compatibility caveats. The `exe_gc_light_hardened` variant is better for compatibility.

The dead-code elimination flags allow the compiler to eliminate unused code, which makes your binaries as small as possible.

### Caveats

Like `exe`, this variant is not suitable for compiling shared libraries. Use the `shlib` variant instead.

### Properties

 * `CFLAGS` and `CXXFLAGS`: `-g -O2 -fvisibility=hidden -ffunction-sections -fdata-sections -fPIE`
 * `LDFLAGS`: `-static-libstdc++ -Wl,--gc-sections -pie -Wl,-z,relro`
 * `STATICLIB_CFLAGS` and `STATICLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden -ffunction-sections -fdata-sections -fPIE`
 * `SHLIB_CFLAGS` and `SHLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden -ffunction-sections -fdata-sections -fPIC`
 * `SHLIB_LDFLAGS`: `-static-libstdc++`
 * `O3_ALLOWED`: `true`
 * Activation command: `/hbb_exe_gc_light_hardened/activate-exec`
 * Activation source script: `/hbb_exe_gc_light_hardened/activate`


## `exe_gc_hardened`

This variant is is meant for compiling applications, but with dead-code elimination and security hardening enabled. This variant is especially suitable for compiling applications for use in production environments.

See [Security hardening binaries](SECURITY-HARDENING-BINARIES.md) for more information about the security flags.

The dead-code elimination flags allow the compiler to eliminate unused code, which makes your binaries as small as possible.

### Caveats

When using this variant, do not use `-O3` because the enabled security features are [not compatible with that optimization level](SECURITY-HARDENING-BINARIES.md).

Some code may not be compatible with security hardening. In that case, use the `exe_gc_light_hardened` variant instead.

Like `exe`, this variant is not suitable for compiling shared libraries. Use the `shlib` variant instead.

### Properties

 * `CFLAGS` and `CXXFLAGS`: `-g -O2 -fvisibility=hidden -ffunction-sections -fdata-sections -fstack-protector -D_FORTIFY_SOURCE=2 -fPIE`
 * `LDFLAGS`: `-static-libstdc++ -Wl,--gc-sections -pie -Wl,-z,relro`
 * `STATICLIB_CFLAGS` and `STATICLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden -ffunction-sections -fdata-sections -fstack-protector -D_FORTIFY_SOURCE=2 -fPIE`
 * `SHLIB_CFLAGS` and `SHLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden -ffunction-sections -fdata-sections -fstack-protector -D_FORTIFY_SOURCE=2 -fPIC`
 * `SHLIB_LDFLAGS`: `-static-libstdc++`
 * `O3_ALLOWED`: `false`
 * Activation command: `/hbb_exe_gc_hardened/activate-exec`
 * Activation source script: `/hbb_exe_gc_hardened/activate`


## `shlib`

This variant is like `exe`, but allows compiling dynamic libraries because the provided static libraries are compiled with `-fPIC`.

### Properties

 * `CFLAGS` and `CXXFLAGS`: `-g -O2 -fvisibility=hidden`
 * `LDFLAGS`: `-static-libstdc++`
 * `STATICLIB_CFLAGS` and `STATICLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden -fPIC`
 * `SHLIB_CFLAGS` and `SHLIB_CXXFLAGS`: `-g -O2 -fvisibility=hidden`
 * `SHLIB_LDFLAGS`: `-static-libstdc++`
 * `O3_ALLOWED`: `true`
 * Activation command: `/hbb_shlib/activate-exec`
 * Activation source script: `/hbb_shlib/activate`
