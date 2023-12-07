# CAFAnaCore Overview

Explanation of the basic classes that build up to a Spectrum, and the flow of information. A more detailed dump of ideas is [here]( https://docs.google.com/document/d/1gLtXQtA64hQvLW3rPmR9Z1wOPya6wjFt64N0xhty6hE)

## Sources and Sinks 

## Information flow for Spectrum / SpectrumLoader

The base `Spectrum` constructor takes a `ValueSource`, which delivers numbers (and exposure information) to the Spectrum.  This is usually a RecordSource<T> (only interface that it delivers objects of some type, e.g. SRProxy) and a Var<T> (turns those into values).

Cuts, weights, systs are implemented by building up a graph of record sources/sinks that apply filtering etc operations. In practice, that means one can write something like
`Spectrum s(src[someCut].WeightedBy(someWei), someVar);`


![CAFAnaCore v2 workflow](https://github.com/mcasales/CAFAnaCore/assets/47826210/16828dbc-7e00-4bee-a63b-db001de61994)
## Example implementation

