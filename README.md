# NEURON Sample Entropy demo readme
written by Sam Neymotin

"Sample Entropy is the negative natural logarithm of an estimate of
the conditional probability that subseries (epochs) of length m that
match pointwise within a tolerance r also match at the next point."

Files:
 sampen.mod - has the Sample Entropy (SampEn) Vector function, vsampen
 vecst.mod, misc.mod, misc.h - support code
 mosinit.hoc - sets up hoc GUI and starts demo

To compile:
 nrnivmodl *.mod

This should generate an architecture-specific directory containing
"special", a script to start NEURON and load the compiled-in
libraries. For example, on x86 64-bit systems, it will make x86_64
directory containing "special"

Then, to run :
 x86_64/special
that will start NEURON
To start the demo, use this command from the NEURON prompt:
 load_file("mosinit.hoc")
mosinit.hoc calls vsampen using its default parameters.

Note that mosinit.hoc calls install_sampen() in the beginning, to make
sure the Vector function, vsampen is available to NEURON.

vsampen Usage:
  Vec.vsampen([epoch length,error tolerance,normalize input,compute
  stdev,output vector])
Vec is a Vector with time-series data
all arguments to vsampen are optional 
epoch length: the number of points to use to match subseries, default:2
error tolerance: the factor * standard deviation of vector to use to
  consider points in subseries a match, default:0.2
normalize: sets Vector to have mean of 0 and standard deviation of 1
  before running sample entropy, default:0
compute stdev:- estimates standard deviation of Sample Entropy
  measure, default:0
output vector: should have size of 2 and stores SampEn and estimate of
  standard-deviation, default:empty
vsampen returns the sample entropy value, which should be >=0. returns
-1 on failure

The code in sampen.mod was used in:
 Interictal {EEG} Discoordination in a Rat Seizure Model by Neymotin,
 SA and Lee, H and Fenton, AA and Lytton, WW Journal of Clinical
 Neurophysiology 27(6):438-444, 2010.
The code in sampen.mod is a NEURON Vector function wrapper over code
written by Doug Lake. Original C code is available from
http://www.physionet.org/physiotools/sampen/
Sample Entropy was first described in:
 Physiological time-series analysis using approximate entropy and
 sample entropy by Richman, JS and Moorman, JR American Journal of
 Physiology- Heart and Circulatory Physiology 278(6):H2039--H2049,
 2000.

For questions/comments, email Sam Neymotin: 
"Neymotin, Samuel (NKI)" <samuel.neymotin at nki.rfmh.org>

