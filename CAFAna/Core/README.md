# CAFAnaCore Overview

Explanation of the basic classes that build up to a Spectrum, and the flow of information. A more detailed dump of ideas is [here]( https://docs.google.com/document/d/1gLtXQtA64hQvLW3rPmR9Z1wOPya6wjFt64N0xhty6hE)

Also see [Doxygen pages](https://cafana.github.io/CAFAnaCore/) 

## Sources and Sinks 
The Source/Sink approach of CAFAnaCore is the basic mechanic of handling information from files and eventually transferring it to something useful, like a `Spectrum`. This is made in order to make `CAFAnaCore` as generic as possible so that each experiment can implement their own `CAFAna` version, and which works independent of the file structure. 

The basic flow of information is pictured here:

<img src="https://github.com/mcasales/CAFAnaCore/assets/47826210/c2daa357-cb07-42d8-adb9-e57670295a5d" width="720">


## Information flow for Spectrum / SpectrumLoader

The base `Spectrum` constructor takes a `ValueSource`, which delivers numbers (and exposure information) to the Spectrum.  This is usually a RecordSource<T> (only interface that it delivers objects of some type, e.g. SRProxy) and a Var<T> (turns those into values).

Cuts, weights, systs are implemented by building up a graph of record sources/sinks that apply filtering etc operations. In practice, that means one can write something like
`Spectrum s(src[someCut].WeightedBy(someWei), someVar);`

## Example implementation

The following diagram shows the implementation in SBN CAFAna, where `SpectrumLoader` is the "pump" ( a `Passtrough` where `SRSpillProxy` is the Source and Sink), that fills all the `sinks` defined in the `Spectrum` (an `IValueSink`).

<img src="https://github.com/mcasales/CAFAnaCore/assets/47826210/0f95cca1-0495-47e7-b2e0-cd182e8e921a" width="900">




