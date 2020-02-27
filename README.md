# cavity-MAP
Maximum a-posteriori estimation for cavity characterisation

### The physics
The Gaussian transversal eigenmodes (TEM modes) of a symmetric optical cavity in a bow-tie configuration with two curved and two flat mirrors (actually, any cavity whose Gaussain TEM eigenmodes have two waists) are completely determined by three out of the following five parameters:
- the (effective) radius of curvature (ROC) of the curved mirrors,
- the shorter distance between the two curved mirrors,
- the longer distance between the two curved mirrors,
- the waist size of the w.l.o.g. smaller of the two waists, centred between the two curved mirrors, 
- the waist size of the larger of the two waists, also centred between the two curved mirrors.

Traversing the optical cavity, the Gaussian light field accumulates a phase depending on the just mentioned parameters, the so-called *Gouy phase*. The effective radius of curvature depends on the angle of incidence of the beam. Non-normal incidence results in two different ROCs for orthogonal planes of the Gaussian beam and in two different Gouy phases. Thus, a fourth parameter enters here, the angle of incidence. The different Gouy phases can be measured. As they depend on the actual physical parameters, these parameters can be estimated from the measurement.

### What we want
- Use data and priors (in our case the measured Gouy phases and our prior beliefs on parameter values) to estimate relevant parameters causing the measurements.

### What we do
With Bayes, we can calculate the probability <img src="https://render.githubusercontent.com/render/math?math=P(p|x)"> of our parameter values <img src="https://render.githubusercontent.com/render/math?math=p"> having caused the measurements <img src="https://render.githubusercontent.com/render/math?math=x">:

<img src="https://render.githubusercontent.com/render/math?math=P(p|x)=\frac{P(x|p)P(p)}{P(x)}">,

where <img src="https://render.githubusercontent.com/render/math?math=P(x|p)"> is given by our model describing the dependency of the measurement on the parameters and <img src="https://render.githubusercontent.com/render/math?math=P(p)"> is our prior belief on the parameters. <img src="https://render.githubusercontent.com/render/math?math=P(x)"> is just a constant normalisation factor and does not affect the optimisation process. Assuming uncorrelated, normally-distributed parameters and normally-distributed data, <img src="https://render.githubusercontent.com/render/math?math=P(x|p)"> is just a product of Gaussian functions.

Maximising the probability over different parameter values (or, rather, minimising the negative logarithm of said probability) leads to estimates for the parameters. This technique is called *Maximum a-posteriori estimation* (MAP). Hence, we are looking for the set of parameters that minimises the negative logarithm of that probability:

<img src="https://render.githubusercontent.com/render/math?math=\min_p\ {-}\log P(p|x)=\min_p\ {-}\log P(x|p)P(p)">.

### Example
The Matlab script minimises the neglog likelihood over the parameters, encorporating beliefs about their distribution. The table shows the results, with all quantities assumed to be normally distributed and their distribution determined by their mean and standard deviation. The first two quantities are measured, the remaining for are estimated.

| Parameter             | Mean     | Std dev | measured/estimated value |
|-----------------------|----------|---------|----------|
| Vertical Gouy phase   |          | 6 deg   | 46 deg   |
| Horizontal Gouy phase |          | 6 deg   | 35 deg   |
| Distance one          | 10.2 cm  | 2 cm    | 10.67 cm |
| Distance two          | 1.45 m   | 0.2 m   | 1.449 m  |
| Radius of curvature   | 100 mm   | 20 mm   | 100.1 mm |
| Angle of incidence    | 3.75 deg | 2 deg   | 3.81 deg |

### Caveat
The results very much depend on the (un-)certainties of our priors. If one of the uncertainties dominates compared to the others, the respective parameter will be the only parameter affected by the
optimisation.
