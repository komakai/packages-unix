# Changelog for [`unix` package](http://hackage.haskell.org/package/unix)

## **TBA**

  * Don't assume non-POSIX `WCOREDUMP(x)` macro exists

  * Don't assume existence of termios constants beyond `B38400`

  * Turn build error into compile warnings for exotic `struct stat`
    configurations (GHC #8859).

## 2.7.1.0  *Dec 2014*

  * Bundled with GHC 7.10.1

  * Add support for `base-4.8.0.0`

  * Tighten `SafeHaskell` bounds for GHC 7.10+

  * Add haddock comments on `RTLD_NEXT` and `RTLD_DEFAULT`

  * Deprecate function `haveRtldLocal`

  * Fix `getGroupEntryForID/getGroupEntryForName` on Solaris. Solaris uses
    CPP macros for required `getgrgid_r` and `getgrnam_r` functions definition
    so the fix is to change from C ABI calling convention to C API calling
    convention

  * Fix potential type-mismatch in `telldir`/`seekdir` FFI imports

  * Use CAPI FFI import for `truncate` to make sure the LFS-version is used.

  * `executeFile`: Fix `ENOTDIR` error for entries with non-directory
    components in `PATH` (and instead skip over non-directory `PATH`-elements)

  * New functions in `System.Posix.Unistd`:
     - `fileSynchronise` (aka `fsync(2)`), and
     - `fileSynchroniseDataOnly` (aka `fdatasync(2)`)

  * New module `System.Posix.Fcntl` providing
     - `fileAdvise` (aka `posix_fadvise(2)`), and
     - `fileAllocate` (aka `posix_fallocate(2)`)

  * Fix SIGINFO and SIGWINCH definitions

## 2.7.0.1  *Mar 2014*

  * Bundled with GHC 7.8.1

  * Handle `EROFS` and `ETXTBSY` as (non-exceptional) permission denied in
    `fileAccess`

  * Fix `getFileStatus` to retry `stat(2)` when it returns `EAGAIN`
    (this can happen on Solaris)

## 2.7.0.0  *Nov 2013*

  * New `forkProcessWithUnmask` function in the style of `forkIOWithUnmask`

  * Change `forkProcess` to inherit the exception masking state of its caller

  * Add new `Bool` flag to `ProcessStatus(Terminated)` constructor
    indicating whether a core dump occured

  * New functions in `System.Posix.Files{,.ByteString}` for operating
    on high resolution file timestamps:

        setFdTimesHiRes :: Fd -> POSIXTime -> POSIXTime -> IO ()
        setFileTimesHiRes :: FilePath -> POSIXTime -> POSIXTime -> IO ()
        setSymbolicLinkTimesHiRes :: FilePath -> POSIXTime -> POSIXTime -> IO ()
        touchFd :: Fd -> IO ()
        touchSymbolicLink :: FilePath -> IO ()

  * Export `SignalInfo(..)` and `SignalSpecificInfo(..)` as well as
    the two `Handler` constructors `CatchInfo` and `CatchInfoOnce`
    from `System.Posix.Signals`

  * Don't export `seekDirStream` and `tellDirStream` if the underlying
    `seekdir(3)`/`telldir(3)` system calls are not available (as on Android)

  * Fix library detection of `shm*` on openSUSE (#8350)

  * Minor documentation fixes/updates

  * Update package to `cabal-version >= 1.10` format

## 2.6.0.1  *Jan 2013*

  * Bundled with GHC 7.6.2
  * Fix memory corruption issue in `putEnv`
  * Use `pthread_kill(3)` instead of `raise(2)` on OS X too

## 2.6.0.0  *Sep 2012*

  * Bundled with GHC 7.6.1
  * New functions `mkdtemp` and `mkstemps` in `System.Posix.Temp`
  * New functions `setEnvironment` and `cleanEnv`
  * New functions `accessTimeHiRes`, `modificationTimeHiRes`, and
    `statusChangeTimeHiRes` for accessing high resolution timestamps
