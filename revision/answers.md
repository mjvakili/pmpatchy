Dear Editor,

We thank the referee for the thorough review of our work and for the constructive report that 
substantially improved the quality of the paper.

Please find below responses to the referee's comments for the submission.

Thank you, Mohammadjavad Vakili & Francisco-Shu Kitaura (on behalf of the authors)

=================================
Reviewer's Comments:

>This paper extends the previous PATCHY code from the authors to include a Particle Mesh (PM) 
algorithm and a MCMC method to fit the halo (or galaxy) bias function from the mass field. 
The paper also provides fit parameters of a particular bias function, and claims that if 
performs better than other fast mock generators, although comparing only with one.

>I would need to see a moderate to major revision of the paper to accept if for publication.

>Main points:

>It seems to me that the main work done here has been integrating two previous public codes (FastPM and EMCEE) 
into the author's code PACHY. I think it needs to be explained how this has been done. 
A section of code integration would be appropriate here.

We agree with the referee's comment and have further explained how different pieces were intefgrated into the 
PATCHY code. In particular, we have added a "Code Integration" section to the paper which in the revised version, is 
section 3. In section 3, we now explicitly state that the positions of particles obtained from the FastPM code are painted
onto a mesh with an interoplation scheme within the PATCHY code. In an MCMC wrapper, the EMCEE code is used to sample from the 
posterior probability. In the MCMC wrapper, everytime a set of PATCHY bias parameters are selected, the PATCHY code populates 
the saved density mesh with galaxies/halos. Furthermore, we explain that for every catalog, power spectrum and 
PDF are calculated and passed to the likelihood function. 

>While the title mention gravity solvers there is parctically no explanation on 
this a part from a reference of Feng et al. This being highlined in the abstract 
and conclusions by the authors it requires a considerable expansion; 
this could be done extending section 2 or a new section.

We have now included more detailed discussion of Particle Mesh gravity solvers in general and FastPM in detail
in subsection 2.1. In particular, we have added four paragraphs describing the basics of particle mesh gravity 
solvers and FastPM. In paragraphs 3 and 4 of subsection 2.1, we explain the structure formation in PM solvers and how it 
differs from more accurate full N-body simulations based on TreePM algorithms that include calculation of force 
on small scales by direct summation of particle pairs. 

Furthermore, in paragraphs 5 we explain the choise of time-steps in PM simulations mentioning 
their drawbacks in terms of small scale accuracy and large scale growth. In pargraph 6, we describe 
how the problem of large scale growth is addressed in FastPM by modifying the PM operations with 
Zeldovich approximation equations of motion.


>It strikes me that the code HALOGEN (Avila et al. 1412.5228), 
when this code basically does the same job. I would require some 
sort of comparison of their performances, even at the level of results 
and not necessarily at the level of using the same Initial Conditions, although
that would be good too.

We have now included a brief discussion of the code HALOGEN in section 2.4 where we discuss comparison 
with other methods. In particular in paragraph 4 of subsection 2.4, we have included HALOGEN in 
the list of methods (PATCHY, EZmocks, QPM) that rely on approximate gravity solvers and stochastic biasing 
schemese for generation of mock galaxy/halo catalogs. 

Furthermore, we have expanded paragraph 5 in order to describe the biasing technique employed in 
the HALOGEN for generation of mocks. After a brief discussion of the biasing technique in the 
code QPM, we describe the main ingredients of HALOGEN: sampling from a mass function, rank-ordering the 
halo mass bins and assuming a bias model for each mass bin, and finally calibrating the bias model 
by fitting the tow-point correlation function. 

In terms of reproducing the distribution of BDM halos in the BigMultiDark simulation, 
Chuang etal. (1412.7729) presents a comparison of different approximate methods including 
ALPT-PATCHY, COLA, EZmocks, HALOGEN, PINOCCHIO, and PTHalos. We have added a paragraph to 
subsection 4.3 to reiterate the fidings of the mock comparison project presented in 
Chuang etal. (1412.7729). 

>All across the paper sentences like "accurate to k= some number" are given. 
These sentences should be complemente by mentining to what degree are 
they accurate lie accurate to X% to k=Y Mpc h^-1.

We have completed those sentences by mentioning the degrees of accuracy.

>Other relevant points:

>Maybe this is trivial, but what is the bivariate halo PDF, does it mean eq 3?

Equation 3 is the deterministic bias relation that determines the expected number 
of halos in a cosmic volume. For each cosmic cell, we then use this bias relation 
to draw a random number of halos from the negative binomial distribution (eq. 5).

The bivariate PDF is a halo statistics which is given by the number of halo counts-in-cells.
In other words, that is the number of cells that host a given number of halos. Alternatively, one 
can think of this as the histogram of the number of halos per cosmic cell. 
We have clarified this in the abstract and in paragraph 9 of introduction 
by adding "counts-in-cells" in parantheses after mentioning bivariate PDF. Furthermore, in paragraph 2 
of Section 2.3 we have now added a sentence to clarify the definition of bivariate halo PDF.

>Section 2.3: is there a reason why the likelihood should be evenly split between 
P(k) bit and rho(n)? What would prevent one to double the number of k bins and 
half the number of density bins? Would you expect the same result?

We have now expanded Section 2.3 to explain the derivation of the log-likelihood term.
We write down the joint probability of powerspectrum and pdf given bias 
parameters as the multiplication of the probability of powerspectrum and probability 
of pdf given the bias parameters. We then assume that each of these probability distributions 
are Gaussian. This leads us to the log-likelihood given in Equation (9).
We have also added another paragraph explaining that the relative weighting between P(k) 
and rho(n) is governed by their corresponding errorbars. More coarse sampling of k 
the errorbar on P(k) larger. Similarly, a more coarse sampling of n, makes the errorbars 
on PDF larger. Giving more weight to the power spectrum makes the results in 
higher stochasticity (higher beta) which leads to higher small-scale power but less 
accurate halo PDF and less accurate bispectrum.

>Section 2.4: "COLA or FastPM computationally too expensive for massive production" 
of next generation of galaxy surveys. Please give details comparing with PATCHY.

We have expanded Section 2.4 to explain why relying only on particle-mesh gravity solvers such as 
COLA or FastPM could be computationaly demanding for massive mock generation. We have added two paragraphs 
to section 2.4 to emphasize that in comparison with PATHCY, methods that make use of PM gravity solvers only 
have to be run with higher resolution (higher gridsize) in order to resolve all the structures/halos. 
We reiterate the findings of Feng etal (2016) and Chuang etal (2015) according to which, the mass resolution of 
PM solvers need to be high to resolve distinct halos.

>Summary:

>"major step" -- better "a move forward towards"

We have changed it to "a move forward towards".

>"previous studies overestimate the contribution of the power due deviation of Poisson" 
-- are these the ALP powers? How clear is this that the reason is the Poisson undersestimation.

>"We have left the analysis of Redshift Space Distortions, as the 2p and 3p are 
more easily described in RSD". ---- This makes no sense. Did you leave the analysis 
for the future because it was more easily dscribed? I understand you don't need to do that, 
just mention it will be presented in future work.

We have changed it to "it will be presented in future work".

>Minor bits:

>Fig 1: mention resolution of ALPT

We mention the resolution of ALPT in the caption.

>Fig 2: mention what the vertical lines are

We expanded the caption to mention that the vertical lines correspond to 68% and 50% confidence intervals of the distributions over the bias parameters of PATCHY.
