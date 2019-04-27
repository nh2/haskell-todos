# nh2's Haskell TODOs

A collection of concrete, not-too-large open-source work items to improve Haskell.

I would appreciate somebody working on them, or funding me to get them done.


## Small

* [ ] Fix all syscalls in `unix` that don't check for EINTR
  * https://github.com/haskell/unix/issues/86
  * https://github.com/haskell/unix/issues/88
* [ ] Fix blocking filesystem operatons in `unix`:
  * https://ghc.haskell.org/trac/ghc/ticket/13296
  * For example, `stat()` is blocking on Linux, so the only way to make it not block the entire Haskell RTS is to make it a `safe` syscall instead of an `unsafe` one
  * `c_stat` called here https://github.com/haskell/unix/blob/312ed2165d04b4c8db7b07133209f69b19b45745/System/Posix/Files.hsc#L174
  * `c_stat` defined as `unsafe` here in GHC: https://github.com/ghc/ghc/blob/945c45ad50ed31e3acb96fdaafb21640c4669f12/libraries/base/System/Posix/Internals.hs#L468-L469
  * The GHC patch that would make this equally fast seems ready, just needs docs: https://phabricator.haskell.org/D1466
* [ ] Implement `O_CLOEXEC`
  * https://mail.haskell.org/pipermail/libraries/2017-June/028073.html
  * Full support from many people, including John Lato and ekmett
* [ ] Implement http://git.savannah.gnu.org/cgit/coreutils.git/commit/?id=24412edeaf556a for `removeDirectoryRecursive`
* [ ] Implement overflow aborts as a GHC option (see https://danluu.com/integer-overflow/ for the cost), then fix all packages
* [ ] Figure out inlining problem in one client project ("p-interface") I worked on (GHC pessimising code)
* [x] Implement system call tracing library in Haskell
  * I did this: [`hatrace`](https://github.com/nh2/hatrace)
* [x] Implement atomic and durable file writes for Haskell
  * We did this with FP Complete ([blog post](https://www.fpcomplete.com/blog/enhancing-file-durability-in-programs))
  * Further improvements using `O_TMPFILE` are upcoming
* [ ] Extract Paypal v2 API I wrote into own package


## Large

* [ ] `numpy` clone with ABI compatibility to numpy, untyped and replicating the entire numpy API
  * numpy is already working to separate the core C libs from the `PyObject` stuff: https://docs.scipy.org/doc/numpy-1.12.0/reference/c-api.coremath.html
  * LumiGuide would be interested in this
* [ ] Finish the SIMD support in GHC and vector
  * https://www.reddit.com/r/haskell/comments/6jlln8/when_competing_with_c_fudge_the_benchmark_xpost/djffyrt/
  * Support by GHC HQ, ekmett


## Things you should probably contract me for

Because I already have almost-working prototypes for this:

* [ ] Making GHC deterministic, producing bit-identical output
* [ ] Solving the `[TH]` recompilation problem
  * [ ] TODO: Publish my writeup of what the problem is


## Bounties

Putting my money where my mouth is, I'll personally pay 500 EUR for any of these to be implemented (coordinate with me first!):

* [ ] Remove all nub, (`\\`), delete and so on functions from GHC and measure the performance on large projects and in nix (where lots of flags are passed)
* [ ] Make all file operations `safe` so they don't block (https://ghc.haskell.org/trac/ghc/ticket/13296)
* [ ] TH recompilation check for ghci (https://ghc.haskell.org/trac/ghc/ticket/4900)
