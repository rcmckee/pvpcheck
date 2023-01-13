# pvpCHECK

# Purpose
Created to check if private repository libraries have a matching public pypi index library name.

Designed to prevent a dependency confusion attack on the PyPi ecosystem.

**Example of attacks:**
- https://www.reversinglabs.com/blog/pytorch-supply-chain-attack-dependency-confusion-burns-devops
<img width="662" alt="image" src="https://user-images.githubusercontent.com/4325493/212239771-56fca957-25d9-49b2-b424-4cc7fb73d944.png">
<img width="732" alt="image" src="https://user-images.githubusercontent.com/4325493/212239896-1d51a3c8-fbf7-4627-b011-a7bc01fd79eb.png">


# Exampe usage:
1. Install
```
pip install pvpcheck
```

2. Mark private repository libraries before lines containing the import statements and after lines containing the import statements.
<img width="536" alt="image" src="https://user-images.githubusercontent.com/4325493/212240938-6adc7d97-fa51-4023-80f8-39a5250acdb6.png">

In a requirements.txt file
```
# check-private-packages-below-for-public-doppelgaenger
os
pandas
example-private-repository-name
# end-of-private-packages
```
In a file_name.py file
```
import os
import pandas
# check-private-packages-below-for-public-doppelgaenger
import example-private-repository-name
# end-of-private-packages
```

3. Run from the command line and provide the path to the file.
```
% pvpcheck -r requirements.txt 
```

If public libraries are found that match your private repository library you will get a response like:
```
WARNING: doppelgaengers found for the following library: pandas
```

*Note: the term doppelgaenger means a biologically unrelated look-alike, or a double, of a living person. I use it here to mean a matching public library that is unrelated to your private library.*
