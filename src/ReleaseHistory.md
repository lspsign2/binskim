# BinSkim Release History
## Definitions
- NR => new rule
- PRF => performance work
- FCR => fingerprint change or refactor
- RRR => rule rename or refactor
- FPC => regex candidate reduction
- FNC => regex candidate increase
- FPS => FP reduction in static analysis
- FNS => false negative reduction in static analysis
- FPD => FP reduction in dynamic phase
- FND => False negative reduction in dynamic phase
- UER => eliminate unhandled exceptions in rules
- UEE => eliminate unhandled exceptions in engine

## **v4.1.0** UNRELEASED
* BUG: Probe local symbols directory for PDBs in all code paths. [828](https://github.com/microsoft/binskim/pull/828)
* BUG: Add missing output in PDB load tracing (enabled by `--trace PdbLoad`. [828](https://github.com/microsoft/binskim/pull/828)

## **v4.0.0**
* BUG: Fix unhandled `ArgumentException` in `Enum.TryParse` on passing `PdbLoad` value to `--trace` command-line argument. [821](https://github.com/microsoft/binskim/pull/821)

## **v4.0.0-rc4**
* DEP: Update Sarif.Sdk submodule from [235394a to 120fae3](https://github.com/microsoft/sarif-sdk/compare/235394a...120fae3). Full [SARIF SDK Release History](https://github.com/microsoft/sarif-sdk/blob/120fae3/src/ReleaseHistory.md).

## **v4.0.0-rc3**
* DEP: Update Sarif.Sdk submodule from [fc9a9df to 235394a](https://github.com/microsoft/sarif-sdk/compare/fc9a9df...235394a). Full [SARIF SDK Release History](https://github.com/microsoft/sarif-sdk/blob/235394a/src/ReleaseHistory.md).
* DEP: Upgrade `Elfsharp.2.16.0` to `Elfsharp.2.16.1`[#791](https://github.com/microsoft/binskim/pull/791)

## **v4.0.0-rc2**
* DEP: Update Sarif.Sdk submodule from [fc9a9df to 90f6a6d](https://github.com/microsoft/sarif-sdk/compare/fc9a9dfb865096b5aaa9fa3651854670940f7459...90f6a6d51dcd3f7df946868360cceb7d7f2f59a0). Resolves performance issues (due to hashing invalid scan targets) and hangs resulting from unhandled exceptions during file enumeration and hashing.
* DEP: Upgrade SARIF-SDK to resolve performance issues (related to hashing invalid scan targets) and hangs (from unhandled exceptions during file enumeration).
* DEP: Upgrade BinSkim to .net6.0 as .net core 3.1 reached end of support on 12/13/2022.
* FPR: Eliminate `BA3003.EnableStackProtector` false positives when the target is statically linked. [744](https://github.com/microsoft/binskim/pull/744)
* PRF: Fix over-aggressive parsing of DWARF compilation units even when all related rules are disabled. [774](https://github.com/microsoft/binskim/pull/774)

## **v2.0.0-rc2** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/2.0.0-rc2)
* BUG: Fix assertion failed with no clue when TargetFileSpecifiers is null or empty for BinSkim analyze.[763](https://github.com/microsoft/binskim/pull/763)
* UER: fix `ERR997.ExceptionLoadingAnalysisTarget : Could not load analysis target` errors analyzing *nix binary resulting from failure to properly parse DWARF debug information.
* DEP: Upgrade `Newtonsoft.JSON` package to 13.0.2 to resolve security alert.

## **v2.0.0-rc1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/2.0.0-rc1)
* BUG: Eliminate `BA2004.EnableSecureSourceCodeHashing` false positives to Windows Runtime components (resulting from references to Win RT API metadata files).
* BRK: Removed SARIF 1.0 support from BinSkim. Now option `-v | --sarif-output-version` does not accept value `OneZeroZero`. [719](https://github.com/microsoft/binskim/pull/719)
* DEP: Update Sarif.Sdk submodule from [fc9a9df to e557b69](https://github.com/microsoft/sarif-sdk/compare/fc9a9dfb865096b5aaa9fa3651854670940f7459...e557b693000cfc2a19d50f2b6613f92222eabbff). Critically, this update resolves transient [`Collection modified`](https://github.com/microsoft/sarif-sdk/pull/2549) exception during analysis. [#722](https://github.com/microsoft/binskim/pull/722)
* FPR: Eliminate `BA2015.EnableHighEntropyVirtualAddresses` false positives for some 32-bit exes. [#721](https://github.com/microsoft/binskim/pull/721)
* NEW: Raw command line passed to the linker now exposed on `ObjectModuleDetail` instances. [#708](https://github.com/microsoft/binskim/pull/708)
* BUG: Fix `error ERR997.ExceptionLoadingPdb : '[filename]' was not evaluated because its PDB could not be loaded (E_PDB_NOT_FOUND).` when reading PE file built with `PDBPageSize:8192` or greater, by upgrading msdia140.dll from `14.27.28826.96` to `14.32.31326.0`. [685](https://github.com/microsoft/binskim/pull/685)
* NEW: Add BA3031.EnableClangSafeStack, rename BA3030.UseCheckedFunctionsWithGcc to BA3030.UseGccCheckedFunctions [#663](https://github.com/microsoft/binskim/pull/663)
* DEP: Upgrade Sarif.Sdk by updating submodule from [fc9a9df to 698adb6](https://github.com/microsoft/sarif-sdk/compare/fc9a9dfb865096b5aaa9fa3651854670940f7459...698adb6365a242c6bb75adde56e3bd4be39c21d7). [#674](https://github.com/microsoft/binskim/pull/674)
* NR : Introduce first performance rule `BA6001.DisableIncrementalLinkingInReleaseBuilds` [#667](https://github.com/microsoft/binskim/pull/667)
* NR : Introduce more performance rules `BA6002.EliminateDuplicateStrings`, `BA6004.EnableCOMDATFolding`, `BA6005.EnableOptimizeReferences`, `BA6006.EnableLinkTimeCodeGeneration` [#691](https://github.com/microsoft/binskim/pull/691)
* BUG: Fix command line parameter in documents: `-Wl,z,relro` with `-Wl,-z,relro`, and `-Wl,z,now` with `-Wl,-z,now`. [736](https://github.com/microsoft/binskim/pull/736)

## **v1.9.5** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.5)
* DEP: Upgrade ELFSharp from 2.14.0 to 2.15.0. [#631](https://github.com/microsoft/binskim/pull/631)
* DEP: Upgrade System.Reflection.Metadata from 5.0.0 to 6.0.1 and System.Collections.Immutable from 5.0.0 to 6.0.0. [#605](https://github.com/microsoft/binskim/pull/605)
* NEW: Enable BinSkim for MacOS. [#576](https://github.com/microsoft/binskim/pull/576)
* DEP: Upgrade Sarif.Sdk by updating submodule from [4e9f606 to fc9a9df](https://github.com/microsoft/sarif-sdk/compare/4e9f606bb0e88428866e253352cdc70dc68f98cb...fc9a9dfb865096b5aaa9fa3651854670940f7459). [#638](https://github.com/microsoft/binskim/pull/638)
* FPR: Skip `BA2025.EnableShadowStack` rule for ARM Binaries which cannot use `/CETCOMPAT`. [#650](https://github.com/microsoft/binskim/pull/650)
* BUG: Fix missing `commandLineId` from `CommandLineInformation` event. [#652](https://github.com/microsoft/binskim/pull/652)

## **v1.9.4** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.4)
* NEW: Add new PE `CV_CFL_LANG` language code for `ALIASOBJ` and `Rust`. [530](https://github.com/microsoft/binskim/pull/530)
* BUG: Fix `BA2014.DoNotDisableStackProtectionForFunctions` to eliminate false positive reports that `GsDriverEntry` has disabled the stack protector. [551](https://github.com/microsoft/binskim/pull/551)
* BRK: Rename `BA2026.EnableAdditionalSdlSecurityChecks` to `BA2026.EnableMicrosoftCompilerSdlSwitch` to clarify rule purpose. [#586](https://github.com/microsoft/binskim/pull/586)
* BUG: Fix `Newtonsoft.Json.JsonSerializationException` when reading SARIF V1 with telemetry enabled. [613](https://github.com/microsoft/binskim/pull/613)

## **v1.9.3** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.3)
* BUG: Fix `KeyNotFoundException` exception raised by `BA2006.BuildWithSecureTools` when individual `MinimumToolVersions` properties are removed from XML configuration. [#565](https://github.com/microsoft/binskim/pull/565)
* BUG: Fix `BA2006.BuildWithSecureTools` is not emitting the compiler list. [Commit SHA 135946](https://github.com/microsoft/binskim/commit/13594680a6ee8beb0ca711d82a7ded2279d3ce4e)

## **v1.9.2** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.2)
* BUG: Fix `MultithreadedAnalyzeCommandBase` artifacts generation and enforcing JSON properties ordering. [#555](https://github.com/microsoft/binskim/pull/555)

## **v1.9.1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.1)
* BUG: Fix incorrect analysis for non-Microsoft compiler on BA2006.BuildWithSecureTools. [#545](https://github.com/microsoft/binskim/pull/545)
* BUG: Fix `JsonSerializationException` that occurs when saving SARIF v1 with telemetry enabled. [#535](https://github.com/microsoft/binskim/pull/535)
* BUG: Fix `NullReferenceException` when `--Hashes` and telemetry rules are enabled. [#531](https://github.com/microsoft/binskim/pull/531)

## **v1.9.0** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.0)

* BUG: Fix telemetry session creation. [515](https://github.com/microsoft/binskim/pull/515)

## **v1.9.0-prerelease3** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.0-prerelease3)

* BUG: Fix exception when collecting telemetry. [486](https://github.com/microsoft/binskim/pull/486), [#487](https://github.com/microsoft/binskim/pull/487)
* NEW: Collect/Send assembly references when rule BA4001 is enabled. [#493](https://github.com/microsoft/binskim/pull/493)
* NEW: Enable multithread analysis. [#495](https://github.com/microsoft/binskim/pull/495)
* NEW: Package `BinaryParsers` project as a new nuget. [#502](https://github.com/microsoft/binskim/pull/502)
* NEW: Do not return 1 when `ignorePdbLoadError` is enabled for PDB loading issues. [#506](https://github.com/microsoft/binskim/pull/506)

## **v1.9.0-prerelease2** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.0-prerelease2)
* BUG: Fix exception handling when PDB cannot be loaded by `IDiaDataSource`. [#461](https://github.com/microsoft/binskim/pull/461)
* BRK: PDB exceptions will be reported once per target. [#465](https://github.com/microsoft/binskim/pull/465)
* BUG: Fix exception `System.AccessViolationException` caused by trying to read data out of boundary. [#470](https://github.com/microsoft/binskim/pull/470)
* BUG: Include C++ runtime in the package to prevent `DllNotFoundException` when loading `msdia140.dll`. [#474](https://github.com/microsoft/binskim/pull/474)
* NEW: Add dialects to the reporting rules. [#475](https://github.com/microsoft/binskim/pull/475)
* BUG: Change compiler report rule to report all modules in file. [#476](https://github.com/microsoft/binskim/pull/476)
* BUG: Fix exception `System.ArgumentException` when checking file format. [#481](https://github.com/microsoft/binskim/pull/481)
* BUG: Fix opcode handling when reading DWARF line number programs. [#482](https://github.com/microsoft/binskim/pull/482)
* BUG: Fix BA3005 to use similar output as BA3003. [#483](https://github.com/microsoft/binskim/pull/483)
* BUG: Fix exception `System.AccessViolationException` when reading DWARF string by position. [#484](https://github.com/microsoft/binskim/pull/484)

## **v1.9.0-prerelease1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.9.0-prerelease1)

* NEW: Add BA3011.EnableBindNow. [#363](https://github.com/microsoft/binskim/pull/363)
* NEW: Add BA2025.EnableShadowStack. [#376](https://github.com/microsoft/binskim/pull/376)
* NEW: Add BA3005.EnableStackClashProtection. [#379](https://github.com/microsoft/binskim/pull/379)
* BUG: Force load PDB. [#380](https://github.com/microsoft/binskim/pull/380)
* BUG: Fix BA2004 for MASM compilers. [381](https://github.com/microsoft/binskim/pull/381)
* NEW: Add BA3006.EnableNonExecutableStack. [#383](https://github.com/microsoft/binskim/pull/383)
* NEW: Add BA2026.EnableAdditionalSecurityChecks. [#388](https://github.com/microsoft/binskim/pull/388)
* NEW: Add BA4002.ReportDwarfCompilerData. [#394](https://github.com/microsoft/binskim/pull/394)
* BUG: Fix for E_PDB_MAX error. [#399](https://github.com/microsoft/binskim/pull/399)
* BRK: Removing win-x86 support. [#401](https://github.com/microsoft/binskim/pull/401)
* NEW: Add baseline support. [#409](https://github.com/microsoft/binskim/pull/409)
* BUG: Fix exception when the PDB is embedded. [#410](https://github.com/microsoft/binskim/pull/410)

## **v1.7.5** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.7.5)
* BUG: Fix import/export config using JSON file. [#349](https://github.com/microsoft/binskim/pull/349)
* NEW: Add compiler report rule BA4001, which is disabled by default. [#350](https://github.com/microsoft/binskim/pull/350)
* NEW: Add support to specific rule documentation in `HelpUri`. [#348](https://github.com/microsoft/binskim/pull/348)

## **v1.7.5-prerelease1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.7.5-prerelease1)
* BUG: Fix import/export config using JSON file. [#349](https://github.com/microsoft/binskim/pull/349)
* NEW: Add compiler report rule BA4001, which is disabled by default. [#350](https://github.com/microsoft/binskim/pull/350)
* NEW: Add support to specific rule documentation in `HelpUri`. [#348](https://github.com/microsoft/binskim/pull/348)

## **v1.7.4** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.7.4)
* BRK: Adding `--verbose` as obsolete which translate to `--level` and `--kind`. [#347](https://github.com/microsoft/binskim/pull/347)

## **v1.7.3** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.7.3)
* NEW: Update SARIF version to latest (using submodule). [#325](https://github.com/microsoft/binskim/pull/325)
* NEW: Add BA2004.EnableSecureSourceCodeHashing. [#320](https://github.com/microsoft/binskim/pull/320)
* BRK: Replace `--verbose` for `--level` and `--kind`. [#339](https://github.com/microsoft/binskim/pull/339)
* BUG: Fix net5 handling. [#345](https://github.com/microsoft/binskim/pull/345)

## **v1.7.2** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.7.2)
* BRK: Revert dotnet-tool. [#316](https://github.com/microsoft/binskim/pull/316)

## **v1.7.1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.7.1)
* BRK: Change from self-contained to dotnettool. [#306](https://github.com/microsoft/binskim/pull/306)
* BUG FIX: Fix issue when analyze `SingleFilePublish` files. [#311](https://github.com/microsoft/binskim/pull/311)

## **v1.7.0** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.7.0)
* DEP: Update to .NET Core 3.1. Changes tool paths in NuGet package.
* NEW: Add `--trace` argument to enable specialized trace of execution behavior, such as `PdbLoad`.
* NEW: Update SARIF version to 2.3.8
* BRK: ** Default output is sarif v2

## **v1.6.1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.6.1)
* DOC: Correct reporting to reflect that /guard:cf is case-sensitive for the compiler. Contributed by [@JacksonText](https://github.com/JacksonTech)
* BUG: Fix ExceptionRaisedInSkimmerCanAnalyze null dereference exception for binaries without PDBs. [#265](https://github.com/microsoft/binskim/issues/265)

## **v1.6.0** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.6.0)
* NEW: Update to final SARIF v2 (version 2.1.16). This enables results caching when passing --hashes on the command-line, a significant performance improvement when recursively analyzing directories with multiple copies of scan targets.
* BUG FIX: Fix typo in BA2021.DoNotMarkWritableSectionsAsExecutable output.
* PERFORMANCE: Eliminate PDB loading for all non-mixed-mode for managed assemblies, including IL Library (ahead of time compiled) binaries.
* FALSE NEGATIVE FIX: Verify that a PDB placed alongside a binary actually matches the binary under analysis
* NEW: Provide --local-symbol-directories argument to specify additional (local, non-symbol-server) PDB look-up locations
* FPR: Skip PDB-driven analysis for the generated .NET core native bootstrap exe (which is not user-controllable code).
* BUG: Drop Spectre analysis to warning
* BUG: Fix Linux NuGet packaging to include BinSkim executable missing in 1.6.0-beta.1
* NRK: Update to pre-release SARIF v2 output format (sarif-2.0.0-csd.2.beta.2019-01-24)
* NEW: Provide for SARIF v1 or v2 file format export. Default is v1 until SARIF v2 is final.
* BRK: ** Output is now Sarif V2-CSD1 compliant rather than Sarif V1  

## **v1.5.1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.5.1)
* BUG: Fix Linux NuGet packaging to include BinSkim executable missing in 1.5.0.

## **v1.5.0** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.5.0)
* Cross platform (Windows/Linux) support.
* BRK: New Results: Identify and fire configuration errors when located PDBs are stripped
* BRK: ** New Results: False negative removed for BA2015.EnableHighEntropyVA:  Correctly flags an AnyCPU binary with HighEntropyVA and Prefer32Bit disabled
* BRK: ** New Rules: New rules for ELF Binaries (BA3001.EnablePieOnExecutables, BA3002.DoNotMarkStackAsExecutable, BA3003.EnableStackProtector, BA3010.EnableReadOnlyRelocations, and BA3030.UseCheckedFunctionsWithGcc)
* BRK: ** New Rules: Provide preliminary BA2024.EnableSpectreMitigations analysis

## **v1.4.5** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.4.5)
* Correct signing check pass message to reflect actual analysis
* Sign all BinSkim binaries

## **v1.4.4** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.4.4)
* Do not fire BA2001.LoadImageAboveFourGigabyteAddressId for ILOnly 64-bit assemblies

## **v1.4.3** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.4.3)
* Fix rich return code return functionality when core command-line parsing breaks
* Export configuration knob to adjust EnableControlFlowGuard linker version check
* Loosen SignSecurely rule to prevent errors on WinTrustVerify errors CERT_E_UNTRUSTEDROOT and CERT_E_CHAINING

## **v1.4.2** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.4.2)
* Add 'rich' return code (a bitfield value of observed runtime conditions) via SARIF SDK --rich-return-code arg

## **v1.4.1** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.4.1)
* Add response file support
* Add __vcrt_trace_logging_provider::_TlgWrite exception to BA2014.DoNotDisableStackProtectionForFunctions

## **v1.4.0** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.4.0)
* Fix rule crash on firing 'not applicable' message for control flow guard check
* Add BinScope readable rule name information to SARIF log file output
* Fix reporting errors when flagging binaries signed with weak cryptogrphic algorithms
* Drop required compiler tools version to 17.0.65501.17013
* Make minimum required linker configurable for EnableControlFlowGuard check

## **v1.3.9** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.3.9)
* Fix false positives of BA2008:EnableControlFlowGuard firing on x86 kernel mode binaries
* Eliminate high-entropy VA analysis for binaries with no entry points
* Update various checks to eliminate noise analyzing boot binaries

## **v1.3.8** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.3.8)
* Update Sarif dependency to 1.5.40
* --config argument is now optional
* Fix false positives of BA2008:EnableControlFlowGuard firing against MC++ mixed mode binaries
* Fix false positives of BA2008:EnableControlFlowGuard firing against resource-only dll that include exported API forwarders (but no code)
* XML-based configuration now functional
* Eliminated compiler tool version false positives for Intel compiler and MASM

## **v1.3.7** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.3.7)
* Update Sarif dependency to 1.5.38
* More incidental reporting improvements

## **v1.3.6** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.3.6)
* Update Sarif dependency to 1.5.36
* Improves output in error cases

## **v1.3.5** [NuGet Package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.BinSkim/1.3.5)
* Fix false positives in 'sign securely' analysis for multi-signed binaries
* Eliminate noise in stack protection analysis against .NET native binaries
* Update Sarif dependency to 1.5.28
* Force load PDBs in some circumstances where they have failed to do so
* Update Sarif dependency to Sarif SDK/Driver 1.5.22-beta (Sarif JSON format 1.0.0)
