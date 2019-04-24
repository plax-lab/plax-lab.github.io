# CASCompCert

The results related to our paper reside in `concurrency/` subdirectory, others are CompCert-3.0.1 files required by our formalization.
Below we list contents of `concurrency/`.

## Top-level files

- [`framework/Soundness.v`](Soundness.html)
> The framework final theorem (Theorem 12)
- [`FinalTheorem.v`](./FinalTheorem.html)
> CompCert correctness with x86-SC backend and object modules (Theorem 14).
- [`x86TSO/FinalTheoremExt.v`](FinalTheoremExt.html)
> Correctness with x86-TSO backend and object modules (Theorem 15).

## Verification framework

- `common/`  
> general definitions, e.g. abstract languages, global semantics, DRF, etc..

    * [`Footprint.v`](Footprint.html)
      > Footprint Definition
    * [`GMemory.v`](GMemory.html)
      > Global memory instantiation
    * [`InteractionSemantics.v`](InteractionSemantics.html)
      > The abstract module-local semantics, including the definition of “well-defined language” (Def. 1)
    * [`GAST.v`](GAST.html), [`GlobDefs.v`](GlobDefs.html), [`GlobSemantics.v`](GlobSemantics.html)
      > Preemptive global semantics (see Fig. 7)
    * [`ETrace.v`](Etrace.html)
      > Event trace definition
    * [`DRF.v`](DRF.html)
      >  Definition of DRF (see Fig. 9 and Sec. 5)
    * [`ReachClose.v`](ReachClose.html)
      > Reach-close (Def. 4)
    * [`Injections`](Injections.html), [`LDSimDefs.v`](LDSimDefs.html)
      > Definitions of footprint matching and rely/guarantee conditions (Fig. 8).
    * [`LDSim.v`](LDSim.html)
      > Module local simulation (see Def. 2, 3). 
    * [`SeqCorrect.v`](SeqCorrect.html)
      > Definition of Sequential compiler correctness (Def. 10)

- `framework/`  
>the verification framework

    * [`NPDefs/NPSemantics.v`](NPSemantics.html)
      > Non-preemptive global semantics (see Fig. 7)
    * [`NPDefs/NPDRF.v`](NPDRF.html)
      > Definition of NPDRF (see Sec. 5) 
    * [`NPDefs/NPEquiv.v`](NPEquiv.html)
      > Equivalence between DRF and NPDRF
    * [`NPDefs/RefineEquiv.v`](RefineEquiv.html)
      > Equivalence between preemptive and non-preemptive semantics of DRF programs (Lemma 9)
    * [`GlobUSim/GlobUSim.v`](GlobUSim.html), [`GlobUSim/GlobUSimRefine.v`](GlobUSimRefine.html)
      > Global upward simulation and the proofs of the Soundness Lemma (Lemma 7)
    * [`GlobDSim/GlobDSim.v`](GlobDSim.html), [`GlobDSim/Flipping.v`](Flipping.html)
      > Global downward simulation and the proofs of the Flip Lemma
    * [`Compositionality/Compositionality.v`](Compositionality.html)
      > Proofs of Compositionality (Lemma 6)

## CompCert verification

- `comp_correct/`
> CompCert verification

    * [`ClightLang.v`](ClightLang.html), [`AsmLang.v`](AsmLang.html), [`SpecLang.v`](SpecLang.html)
      > Clight, x86-SC, and CImp language instantiations
    * [`ClightWD.v`](ClightWD.html), [`AsmWD.v`](AsmWD.html), [`SpecLangWDDET.v`](SpecLangWDDET.html)
      > Proofs showing that Clight, x86-SC, CImp languages are well-defined 
    * [`AsmDET.v`](AsmDET.html), [`SpecLangWDDET.v`](SpecLangWDDET.html)
      > Proofs showing that x86-SC and CImp are deterministic  
    * [`localize/Localize.v`](Localize.html)
      > Lifting lemmas for reusing CompCert's proofs
    * [`localize/LDSim_local_transitive.v`](LDSim_local_transitive.html)
      > Transitivity of the CompCert memory based simulation
    * [`SpecLangIDTrans.v`](SpecLangIDTrans.html)
      > Correctness of the identity transformation of CImp modules
    * [`CompCorrect.v`](CompCorrect.html)
      > The adapted CompCert compiler and its correctness proof (Lemma 13)
    * `cfrontend/` and `backend/`
      > Instantiations of the intermediate languages (`*_local.v`)
      > Below is the list of proved individual compilation passes, 
      	along with its code and correctness proof

    | Intermediate Languages | Instantiation                                     |
    | ---------------------- | ------------------------------------------------- |
    | CSharpminor            | [`Csharpminor_local.v`](./Csharpminor_local.html) |
    | Cminor                 | [`Cminor_local.v`](./Cminor_local.html)           |
    | RTL                    | [`RTL_local.v`](./RTL_local.html)                 |
    | LTL                    | [`LTL_local.v`](./LTL_local.html)                 |
    | Linear                 | [`Linear_local.v`](./Linear_local.html)           |
    | Mach                   | [`Mach_local.v`](./Mach_local.html)               |

    | Pass          | Compiler code                         | Correctness Proof                                 |
    | ------------- | ------------------------------------- | ------------------------------------------------- |
    | Cshmgen       | [cshmgen.v](cshmgen.html)             | [cshmgen_proof.v](cshmgen_proof.html)             |
    | Cminorgen     | [cminorgen.v](cminorgen.html)         | [cminorgenproof.v](cminorgen_proof.html)          |
    | Selection     | [selection.v](selection.html)         | [selection_proof.v](selection_proof.html)         |
    | RTLgen        | [rtlgen.v](rtlgen.html)               | [rtlgen_proof.v](rtlgen_proof.html)               |
    | Tailcall      | [tailcall.v](tailcall.html)           | [tailcall_proof.v](tailcall_proof.html)           |
    | Renumber      | [renumber.v](renumber.html)           | [renumber_proof.v](renumber_proof.html)           |
    | Allocation    | [allocation.v](allocation.html)       | [alloc_proof.v](alloc_proof.html)                 |
    | Tunneling     | [tunneling.v](tunneling.html)         | [tunneling_proof.v](tunneling_proof.html)         |
    | Linearize     | [linearize.v](linearize.html)         | [linearize_proof.v](linearize_proof.html)         |
    | CleanupLabels | [cleanuplabels.v](cleanuplabels.html) | [cleanuplabels_proof.v](cleanuplabels_proof.html) |
    | Stacking      | [stacking.v](stacking.html)           | [stacking_proof.v](stacking_proof.html)           |
    | Asmgen        | [asmgen.v](asmgen.html)               | [asmgen_proof.v](asmgen_proof.html)               |

## Extended framework 

- `x86TSO/` 

    * [`AsmTSO.v`](AsmTSO.html)
      > The x86-TSO language instantiations
    * [`ObjectSim.v`](ObjectSim.html)
      > Object simulation
    * [`TSOCompositionality.v`](TSOCompositionality.html)
      > Proof of Lemma 16 (Restore SC semantics for DRF x86 programs)
    * `lock_proof/`
      > An efficient spin-lock implementation ([`code.v`](code.html)) with its correctness proof ([`LockProof.v`](LockProof.html))
