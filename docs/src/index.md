```@meta
CurrentModule = PseudoLibraries
```

# PseudoLibraries

Enables programmatic access to
standard pseudopotential libraries in solid-state calculations.
In using this library the combination of a string identifier and the element
symbol provides a unique and reproducible mapping to a pseudopotential file.
Moreover in case the pseudopotential file
happens to be missing on the computer Julia's artifact system takes
care to automatically download it as needed.

## Basic usage

For example, the following code automatically downloads the pseudopotential
file of the [stringent pseudodojo](http://www.pseudo-dojo.org/) pseudopotential
for LDA pseudopotentials (referred to by the identifier `pd_nc_sr_lda_stringent_0.4.1_upf`)
and places the full path to the downloaded pseudopotential file into the `filename` variable:

```@example index-example
using PseudoLibraries
identifier = "pd_nc_sr_lda_stringent_0.4.1_upf"
library = PseudoLibrary(identifier)
filename = library[:Si]
```
As you see this will be a string such as
`/home/user/.julia/artifacts/56094b8162385233890d523c827ba06e07566079/Si.upf`,
which luckily you don't usually have to know or remember.
Note, further that this path may differ between computers,
julia versions etc.
It is therefore highly recommended to use the above mechanism
based on `identfier` and element symbol instead of hard-coding
the expanded path in user scripts.

An alternative version to achieve the same thing as above is
```@example index-example
filename = pseudofile(library, :Si)
```
or for multiple elements:
```@example index-example
pseudofile.(library, [:C, :Si])
```

Some metadata information is stored in the `library` object:
```@example index-example
library
```

For a list of available identifiers see
```@example index-example
PseudoLibraries.available_identifiers()
```
More details on the meaning of these keys is given
in the README of thei
[PseudoLibrary](https://github.com/JuliaMolSim/PseudoLibrary/blob/7c4b71a3b9d70a229d757aa6d546ef22b83a85a9/README.md)
repository.

!!! warning "Rename of pseudopotential identifier reserved"
    The current identifiers for the pseudopotential families is planned to be overhauled.
    This will be a breaking change, where the minor version of the package will be bumped.

## Interface

```@autodocs
Modules = [PseudoLibraries]
```
