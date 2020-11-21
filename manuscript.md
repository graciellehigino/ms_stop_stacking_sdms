---
bibliography: [references.bib]
---

## Introduction  

The occurrence of a species in a given location is an encrypted message that
travels through time. It carries the species' evolutionary history, long
migration journeys, effects of other species we do not even know that exist, and
ultimately the elements that shape its, yet unknown, future. Ecologists have
been trying to decode this message with progressively more powerful tools, since
their own field notes to highly complex computational algorithms, such as
habitat suitability models. These models were born as an attempt to model
species' distribution based on their niche, considering their occurrences as
sample points of suitable abiotic variables and their absences as sample points
of unsuitable variables. However, these observations (environmental variables
and geographic location) only unveils part of the mystery, and the missing link
are ecological interactions. Habitat suitability models (hereafter HSMs) can be
untangled in three aspects of a species occurrence: its biotic environment - the
connections it makes with other species -, its abiotic environment - the
connection it makes with non-living resources -, and its mobility range - how
far it can go (@fig:bam)[@Peterson2012EcoNic]. The biotic environment act on
these models as potential and realized interactions, constrained or enabled by
abiotic factors, geographical conformation and migratory ability.   

![The "BAM diagram", adapted from [@JorgeSoberon2007GriElt]. Open circles
are absences and solid circles are observed presences. Big circles correspond to
the theoretical space of a species, regarding its biotic interactions (the B),
the abiotically suitable space (the A) and the geographic area accessible to it
(the M). These three aspects represent real points of occurrence on the real
geographic space (the G). Ecological interactions act over this model in four
ways: in (1), there are potential interactions that are never realized because
of geographical and environmental constraints; in (2) interactions are realized
on accessible, abiotically suitable areas; the space (3) is where the species
could eventually go and establish new interactions, while (4) is the area where
the occurrence of the species is limited only by abiotic factors.](figures/bam.png){#fig:bam}  

Accounting for environmental variables and geographic limits on biodiversity
distribution models is a good approach because these characteristics are not
(highly) dynamic entities from the evolutionary point of view. Because the
climate (used to) change at a very slow pace, as well as species' niche, we
could expect to find the same pool of species that are able to live in a certain
region, even if populations fluctuated at a smaller temporal scale. This is
because the cumulative effect of small scale variation on climate, population
dynamics and habitat suitability itself results in macroecological outcomes such
as combinations of extinction and cladogenesis, which lead to biodiversity
distribution at continental scales. Also, abiotic variables are not under the
influence of the focus species, which make them statistically safe, and their
relationship with the species' niche is assumed to be static in space and time,
which adds generalization to the model. The biotic space, on the other hand, is
usually highly dynamic and variable, and it can be stochastic at very small
scales to predictable structures at large scales. Additionally, because
ecological networks are the cumulative result of local events
[@Poisot2016HowEco; @Guimaraes2020StrEco], its properties can vary with
environmental factors and species evolutionary history
[@MartinGonzalez2015MacPhy; @Dalsgaard2013HisCli].  

There is a big ecological and evolutionary leap between local dynamics of
species and the biogeographical processes that are the primary assumptions to
the habitat suitability and species distribution models. However, because
ecological networks are very informative and aggregate populations' dynamics
through scales, it is conceptually important to include them in HSMs. In fact,
it has been shown that HSMs are more efficient when ecological interactions are
accounted for (either directly or indirectly) [@Wisz2013RolBio;
@Cazelles2016IntBio]. Some strategies have been adopted by the scientific
community to accomplish that and are shortly reviewed later in this paper.
Correlative approaches assume that the co-ocurrence of related species accounts
for interaction, while mechanistic models try to refine this assumption by
species traits and phenology. Currently, the scenario of habitat suitability
models accounting for the biotic environment is either too generalistic
(correlative approaches) or too precise (mechanistic), in the sense that they
only work when we have a good amount of information about that specific species.
However, empirical data on ecological interactions are scarce, and, on the other
hand, we cannot just assume that two species will always interact when they
co-occur. How could we find balance and go further?

The good news is that ecologists have been developing techniques to predict and
forecast the ecologically realistic number of links [@MacDonald2020RevLin], the
nature of ecological interactions [@Elmasri2020HieBay], and networks' properties
with good accuracy. These techniques can mitigate the large and biased eltonian
shortfall that we have now [@Poisot2020EnvBia; @Hortal2015SevSho]. In this
context, we can envision an integrative approach of species distribution
modelling combined with network prediction resulting in a more realistic, yet
generalist, model where the predicted networks update the probabilities of
occurrence computed by an HSM. In this paper we invite you to envision better
species distribution models, which do not ignore our knowledge about ecological
networks and communities assemblage. Here we suggest this can be done with the
help of machine learning techniques both to predict local networks and to update
the results of grinellian HSMs. We point to promising directions on the
development of these techniques and main challenges ecologists might face in the
near future.

![TODO](figures/concept.png)

## HSMs: the mechanics, innovations and drawbacks  

Habitat suitability models aim at finding relationships between the occurrence
of species and their environment [@Guisan2000PreHab; @Guisan2017HabSui]. The
reader might have encountered different terminologies in this area, such as
species distribution modelling and ecological niche modelling, that supposedly
have the same objectives. The terminology is a matter of debate on the
scientific community, and here we chose to distinguish habitat suitability
models from species distribution models.  

Ecological niche models and habitat suitability models focus on the the area of
A of the BAM diagram [@fig:bam] where a species can occur, which means they
calculate the fundamental niche of species [@Peterson2012EcoNic]. This can be
achieved by finding the relationship between environmental conditions and the
presence or absence of a certain species. This relationship can be static or
dynamic in space, and only makes sense when calculated for the area inside M.
Therefore, this means that they will find suitable areas inside the area 2,
where species really are, but can also find suitable areas in 5, where the
species probably are not because of biotic unsuitability. Species distribution
models, on the other hand, should aim at modelling 2 (B $\cap$ A $\cap$ M), which
means considering biotic constraints [@Peterson2012EcoNic]. Although they rarely
do so, Guisan and Zimmermann (2000) argue that the observation data used as
input on these models carries these information: when we use the physiological
limits of a species as a variable to be correlated to the environment, we are
modelling its fundamental niche, while using observational field occurrence data
implies that we are modelling the realized niche (thus, the species
distribution) because these data implicitly accounts for biotic limitations
[@Guisan2000PreHab]. However, because the biotic constraints are not explicitly
considered in the models, it is possible that the predicted distribution area
reaches places with completely different communities. Because we did not
consider previous knowledge about species interactions, how can we interpret
this result? Given these differences between SDMs and HSMs, many statistical
approaches can be used to model both of them. Here we focus on the most
innovative algorithms to find the species' suitable habitats, to further develop
ideas on how to integrate biotic constraints.

Habitat suitability models are built over five steps: conceptualization, data
sampling, calibration, evaluation and prediction [@Guisan2017HabSui]. The
conceptualization is related to the core ideas of niche, as illustrated in
@fig:bam, but also to the main goals of the investigation. What processes are
important to the patterns we a dealing with, what is the frequency in which they
repeat in space (determining the grain and extent of the environmental
variables) and what are the direct and indirect predictors are examples of
questions that should be asked at this step. The answers to these questions will
determine how the data should be sampled (the spatial scale of the variables)
and the appropriate selection of the variables [@Guisan2000PreHab]. Then the
actual building of the mathematical model enters the stage, with iterative
adjustments to capture its variations. The data is separated in training
validation sets, and then the model is used to predict and project probabilities
is space that can be interpreted as habitat suitability.

<!---innovations--->
While statistical inference is a telescope that allows us to investigate the
past of biodiversity structure, machine learning algorithms are some of the time
machines we use to assess the past in order to predict the future. They have the
power to learn from the data, identifying structure and generating predictions
[@Olden2008MacLea]. One sound advantage of these models compared to statistical
inference is that they allow us to explore "mischievous" data, embracing the
multiple frequency distributions we find in nature. Many of them have become
popular among ecologists, such as MaxEnt [@Phillips2006MaxEnt] and Random Forest
[@Breiman2001RanFor], while making a good match with the continuously growing
amount of biodiversity data. Although these models call for cautious usage for
their complexity (and hard to interpret outputs) [@Rangel2012LabEco], it also
demands some ecological knowledge about the relationships being modelled and
careful parameterisation of terms. These very characteristics are the ones that
allow us to explore nuances of biodiversity relationships, such as the role of
ecological interactions in shaping species distribution - i.e. putting the B
back in the BAM model.     

<!---drawbacks--->
However, these time machines need a past to learn from, and the lack of
information about species interactions makes this past quite blurry. Ecological
interactions occur across taxonomic and geographic scales
[@Guimaraes2020StrEco], and the task to collect these information through large
extents and in fine grain (both temporal and spatial) is daunting. In addition,
it is known that networks vary with climate, in space and with phylogenetic
distance [@Poisot2014SpeWhy; CITATIONS]. Despite the dynamic nature of networks'
structures (that are predictable outcomes of common processes), methods such as
stacked (S-SDMs) and joint Species Distribution Models (JSDMs) are very common
to address the influence of one species over another [CITATIONS]. These methods
assume that, if a pair of species are known to interact, they will always do so
once they co-occur [CITATIONS]. For example, in order to do a stacked SDM, one
can model the assembly as a single unit, use the predicted distribution of each
species and pile them up together, or model species at the same time, but as
separate units [@Ferrier2006SpaMod]. On the other hand, JSDMs use a hierarchical
regression model to calculate the probability of occurrence of all species
together in response to environmental variables [@Pollock2014UndCoo]. Both
approaches can be considered great advances regarding previous methods that
simply added the distribution of one or more other species as limiting factors
in the model [CITATIONS]. S-SDMs and JSDMs try to incorporate another level of
complexity by modelling assembly rules as an intermediate step towards more
realistic HSMs (see @Zurell2020TesSpe for a comparison between both methods).
Nevertheless, our time machines can take us even further and incorporate actual
species interaction and predicted network properties in species distribution
models.  

## Going further  

<!---why interactions in SDMs--->
Spatially structured co-occurrence can be the result of many historical and
geographical processes, such as environmental heterogeneity and the similarity
of environmental preferences between species [@Bar-Massada2017NonCoo]. HSMs that
account for co-occurrence as a proxy for interactions might wrongly capture
these processes as biotic interactions [@Blanchet2020CooNot]. An important
analysis to be made before going further is at which scale ecological
interactions influence the distribution of species. Although empirical evidence
exists that ecological interactions are important processes on population
arrangements in space [CITATIONS] and networks variation can be detected in
macroecological scales [CITATIONS], their precise relationship with spatial
scale remains unclear. A second challenge is to deal with highly dynamic
properties of ecological interactions. How can we account for dependency between
local processes in macroecological scales? We argue that Artificial Intelligence
(AI) tools can help us identify structure on the available data and predict
interactions and networks for communities we did not access yet.

### The Eltonian Noise paradox  

The Eltonian Noise Hypothesis states that the effect of ecological interactions
on species distribution is captured at coarse resolution analyses as a
covariation with environmental factors [@Soberon2009NicDis]. This logic reverts
as an assumption that always that two given species co-occur, they will
interact, which has been demonstrated to be not true [@Blanchet2020CooNot]. In
fact, the contrary is likely to be true: the nature of interactions happening at
a given location affects co-occurrence [@Bullock2000GeoSep; @Chesson2008IntPre;
@Godsoe2012HowSpe; @Svenning2014InfInt; @Godsoe2017IntBio], and they vary in
space and time due to climate change, phylogenetic diversity (addition or
extinction of clades in the community, for example)[@Davies2011PhyDiv],
population density [@Carnicer2009TemDyn], and many other factors. Additionally,
analyses of range expansion rates - a common and very important application of
HSMs - are intrinsically connected to interspecific interactions at the border
of the ranges: the expansion tends to be slower when generalists predators are
present or when mutualists are absent [@Svenning2014InfInt]. On the other hand,
range preservation is also associated with ecological interactions, once
connected species can be protected of climate change and invasion
[@Dunne2002NetStr; @Memmott2004TolPol; @Ramos-Jiliberto2012TopPla].  

This hypothesis also seems to find no support when we investigate the
betadiversity of links in ecological networks. In parasite-hosts systems in
Eurasia, it is possible to detect a distinct difference in interactions between
shared species in macroecological scale, suggesting an "unpacking" of species
when biodiversity is expected to be lower [CHAPTER 1]. In addition, it is
likely that species with larger ranges of distribution and those that are more
generalists would co-occur with a greater number of other species
[@Dattilo2020SpeDri], while dispersal capacity of competitive species modulate
their aggregation in space and the effect of interactions on their range limits
[@Godsoe2017IntBio].  

Certainly, the exact macro scale effect of interspecies interactions might
depend on the nature of these interactions, the system being studied and the
combination of geographical and environmental factors. Younger communities may
be more affected by environmental limitations, once they are dominated by
generalist species, while older metacommunities are probably affected in
different ways in the centre of the distribution, at the edge of ranges and in
sink and source communities. In fact, there is a growing number of evidence
demonstrating that biotic interactions are important factors modulating range
shift and expansion due to rapid climate change (where evolutionary processes
are ignored, assuming that species will not have time to adapt)
[@Bullock2000GeoSep; @Hellmann2012InfSpe; @Afkhami2014MutEff; @Godsoe2017IntBio;
@Siren2020IntRan].  

Modelling species distribution considering the Eltonian Noise Hypothesis to be
true can be very useful to understand general structures of biodiversity. At
coarse resolutions, with dubious quality and sparse data, and when the space for
error is large, these models are probably the best we can do. However, no species is an
island and we should go further whenever possible, investigating whether and how
ecological interactions exert important pressures on species ranges and spatial
arrangements. This will help us avoid spurious inferences, especially when these
models aim at conservation strategies. Fortunately, the data we need to do that
has been increasingly available [@Konig2019BioDat], and technologies to deal
with them (with their biases and gaps) are following.  

### Non-stationarity of interactions and networks in space, time and across resolutions  

Ecological interactions are dynamic entities of ecosystems that vary in space
and time. The reason for this fluctuability is a combination of factors that
shape the probability of interactions: environmental changes that affect the
metabolism of individuals and the abundance of populations [@Rall2012UniTem;
@Poisot2016StrPro; @Muola2010AssPla], changes in habitat
[@Tylianakis2017EcoNet], and the phylogenetic structure of communities
[@Coelho2017NeuBio]. Notably, the variation in traits distribution (including
phenological mismatches) are important drivers of variation in species
interactions [CITATIONS].  

Ecological networks reflect these dynamics, and, as a result, varies in space
not always in the same fashion that species richness do [@Poisot2014SpeWhy]. The
non-stationarity of ecological networks and their relationship with the
environment can be measured and have been demonstrated in the last few years.
@Dalsgaard2013HisCli found that modularity can be reduced and nestedness
increased due to climate change speed [@Dalsgaard2013HisCli]. The phylogenetic
diversity of networks is affected by dispersion and speciation rates
[@Coelho2017NeuBio; @Sebastian-Gonzalez2015MacTre; @Trojelsgaard2013MacPol],
characteristics highly correlated to both traits and geographical structure of
the environment. These examples illustrate how networks can vary both in space
(due to environmental filtering of species traits, for example) and time (due to
evolutionary changes and phenology).  

Interestingly, because ecological networks are the cumulative pool of local
interactions, it is possible that network structure varies across scales
[@Galiana2018SpaSca]. For example, increased species richness can promote
species packing and specialization of interactions at local scale even for
generalist species [CITATIONS; CHAP 1]. Moreover, the local combinations of
species and interactions in a community can result in very different regional
pictures, since interactions can affect one another. For example
@Sanders2012IndCom observed that the persistence of two species of wasps
separated by four trophic links are conditioned to one another because they
regulate the population of competitive aphids [@Sanders2012IndCom]. The
replacement of one species in this network can result in the local extinction of
another, even if they are not directly linked, and this dynamic could be easily
misinterpreted in regional scales as an environmental constraint.

All these peculiarities about ecological interactions and networks can be faced
as challenges or opportunities for the next years. Once we understand how and
where interactions are important to the accuracy of species distribution models,
we can use the dynamics described here as refinements on our models. On the
other hand, some of these mechanisms act at a scale so small that stochasticity
takes the stage and can be accounted for in the error term of most models. This
trade-off reinforces the need to carefully adjust distribution models according
to the system being studied.

### Why we can go further  

A combination of global efforts and technology can make us take another step in
combining species occurrence data and ecological interactions. In the last
decades we have witnessed an increase in biodiversity data, including
citizen-science projects [@Pocock2015BioRec; @Callaghan2019ImpBig] and organized
dedicated databases mostly accessed by specialists, such as mangal and GBIF
[@Poisot2016ManMak; @Gbi]. These data frequently describe the occurrence and the
taxonomic identity of a species, but they also capture real-time interactions
[@Roy2016FocPla; @Ryan2018RolCit]. Moreover, both occurrence and interaction
data share common characteristics that can be learned and subsequently inferred.
Because species occurrence are subject to their evolutionary history that shaped
their ecological niche, one can roughly infer where it could occur only based on
known occurrence point locations (that is how HSMs work, as described earlier in
this paper). This is connected to how ecological networks also show signs of
common ancestry and preserve a basic structure [@Riva2016ExpEvo; @Dallas2018ComTur]. The
ever-growing number of available data and detectable structure on ecological
networks are the main ingredients we need to develop mathematical models capable
of learning from what we already know to predict what we do not know yet.

#### Filling in eltonian gaps with mathematics: predicting interactions, networks, and doing it across scales  


A complete assessment of ecological interactions is even more difficult than
sufficient sampling of biodiversity. The number of interactions sampled will
always be lower than the number of possible interactions, mainly due to the
existence of forbidden links [@Jordano2016SamNet]. This lack of information,
known as the Eltonian Shortfall, is aggravated by biases and differences in
sampling methods [@Hortal2015SevSho]. Nevertheless, in the same way as the
knowledge about the natural history of organisms help us validate HSMs,
understanding a species' behaviour, traits and phylogenetic relationships can
help us identify if the lack of links sampled is due to insufficient effort or
natural mismatch between species. Additionally, interactions vary in space and
time, which adds to the uncertainty of an unregistered interaction. Hence,
rather than assuming interactions to be binary variables, we can think of them
as probabilities [@Poisot2016StrPro]. In fact, assuming interactions as
probabilistic events is more of an opportunity than an obstacle. Once we
understand what is the basic mix than can result in a connection between
ecological units (from individuals to ecosystems), we can use probabilities to
estimate the likelihood of our ideas even when data is lacking. Usually, this
basic mix is composed by abundance, co-occurrence in space and time (conditional
to a given environment), and traits matching [@Poisot2014SpeWhy; CITATIONS]. The
regional pool of interactions also plays an important role on interactions
realization through indirect effect [@Sanders2012IndCom; @Poisot2014SpeWhy], but
they also add another layer of complexity in predictive models.  

When we do not have information about any of these properties, interactions tend
to behave as stochastic elements in our model, while the more information we
have, the more our equations will look like a niche model. Maybe one of the most
neutral approaches to predicting interactions is assuming that two species will
always interact once they co-occur. On possible step forward is to account for
spatial structure of species distribution: interactions are more or less likely
to occur according to the location of the population inside the species range
[@Svenning2014InfInt; @Godsoe2017IntBio; @Bar-Massada2017NonCoo]. Moving away
from stochasticity a little bit, @Canard2012EmeStr illustrates how we can build
neutral networks based on species abundance and richness, and found that the
emergent properties of these networks are compatible with empirical ones. With
this method, it is possible to identify neutral forbidden links
[@Canard2012EmeStr], which unfolds many other questions that can be answered
without previous empirical data. For example, we can investigate whether
abundance fluctuation is the main driver of betadiversity of links between
networks, or compare how networks are different from the neutral model when only
the traits vary. It is important to notice, however, that abundance also plays a
role on the nature of the interaction. Mutualistic interactions, for example,
can turn into parasitism or competition when one of the players is very abundant
[@Wolin1984ModFac].  

An intermediate step could be to find detectable interactions in a species pool.
@XiaoFu2019LinPre proposed a combination of a Poisson N-mixture model and
collaborative filtering to predict potential links under imperfect detection.
This machine learning model allowed them to successfully infer interactions
based on a few observed occurrences sampled in the field [@XiaoFu2019LinPre].
This approach deals with interactions as countable units, ignoring evolutive and
ecological mechanisms that could lead do variation in the probability of their
realization. However, it can be a good exploratory method to investigate the
completeness of interaction sampling.  

On our way to more mechanistic models, we can start looking for evolutionary
clues on our encrypted message. First, we can assume that similar species will
interact in similar ways with their "pairs" due to phylogenetic inertia
[@Gomez2010EcoInt; @Peralta2016MerEvo]. If predators *A* and *B* are closely
related, they are likely to compete for the same set of preys. In this sense, we
can use machine learning algorithms to find in the "potential interactions" pool
those that are more ecologically likely to occur. For example,
@Desjardins-Proulx2017EcoInt showed that the *K* nearest neighbour (KNN) and the
Random Forest (RF) algorithms are complementary when it comes to identifying the
probability of a predator to interact with a certain prey and binary occurrence
of interactions (RF predicts either interaction or non-interaction)
[@Desjardins-Proulx2017EcoInt]. According to the authors, the usefulness of
these methods depend on the kind of data we have in hands: KNNs need previous
information about interactions to learn from, while RFs should use a set of
traits. Another example of link prediction based on trait matching is
@Dallas2017PreCry, where the authors identified cryptic associations between
hosts and parasites based on a Bayesian model. Similar to @XiaoFu2019LinPre
model, this model also allow us to investigate the completeness of interaction
sampling, but now based on traits matching and not only on occurrence
observations. @Pichler2019MacLea provide an extensive methodological comparison of
Machine Learning models to predict interactions based on traits matching.
Nonetheless, these techniques isolate interactions from their biotic and abiotic
environments, and this should be kept in mind whenever predictions are made.  

Another step further would be implementing evolutionary models in the
relationship between links and phylogeny. @Elmasri2020HieBay point out that
recent approaches to link prediction using phylogenetic similarity assume a
linear or fixed diversification rate. They proceed to develop a phylogenetic
matching model of predicted interactions using the early-burst tree scaling
model, where the traits diversification tree is transformed, adjusted by a
single parameter, either to early or late diversification [@Harmon2010EarBur;
@Elmasri2020HieBay]. The authors also accounted for uncertainty in unobserved
interactions, which improved the accuracy of the predictions. The adjustment of
the early-burst parameter can be based on ecological reasoning. For example,
food webs with species clustered in trophic levels (specialized predators, for
example) seems to have a trait evolution with a high diversification rate early
in the tree, while networks with many omnivorous species are thought to have a
late diversification of traits [@Ingram2012WheSho]. These predictions are highly
mechanistic, accounting for evolution and ecology of interactions.  

Connected to the Eltonian Shortfall described at the beginning of this session,
there are global gaps and biases on network sampling [@Poisot2020EnvBia].
Because ecological networks are made of nodes and edges, and both can be treated
as probabilities (addressing the occurrence of a node and the realization of an
interaction), we can investigate the chances of different networks to emerge
from a set of species co-occurring in a given location [@Poisot2016StrPro].
Recently, @MacDonald2020RevLin demonstrated how we can estimate the number of
possible links in a network based on the number of species it has, which take us
closer to predict networks themselves since we have much more information about
species than we have of interactions [@MacDonald2020RevLin]. Knowing the number
of possible links given the species richness in a given location allow us to
calculate the probability distribution for each network property, which can be
further connected to what we know about the relationship between networks'
properties and species spatial distribution

One question that is frequently stressed by macroecologists is how to connect
local processes, such as interactions, to large scale biodiversity structures.
The sampling of both interactions and environmental variables are usually made
in opposing ends of spatial resolution, which makes them incomparable from a
statistical point of view [@Peterson2012EcoNic]. Also, because of the nature of
the sampling, it is hard to transform those variables to make them vary in
compatible scales. How can we deal with this problem when predicting
interactions and networks for macroscales? In fact, the basic mix components
that leads to the occurrence of an interaction varies with the spatial
resolution in which it is assessed. Consequently, the distribution of
probabilities for interactions and network properties would change, possibly
leading to different interpretation of biodiversity distribution. However, the
different ways in which networks properties vary through scales have also been
investigated, and simulations can help us understand that more deeply
[@Poisot2014SpeWhy; @Peralta2016MerEvo; @Guimaraes2020StrEco]. *Because*
interactions vary more in space than species occurrence (while adding to this
information) [@Poisot2017HosPar], they can represent biodiversity with a more useful
macroecological variance to interplay with environmental variables. Moreover,
because interaction predictions accounts only for *potential interactions*, they
are easily translated into regional networks (that also represent potential
interactions). Finally, some properties of networks are correlated to the
phylogenetic diversity of communities [CHAP 1], which also represents a level of
organization compatible with the geographical scale of environmental variables.  

#### Updating probabilities of occurrences with network probabilities  

At this point the reader may be wondering how probabilistic networks and species
distribution models fit together. Some efforts in this sense have already been
made, and in this session we will quickly review them while pointing to future
directions. We will not consider, however, the majority of papers that aim at
discussing the integration of biotic interactions on SDMs because their
definitions of ecological interactions are not compatible with our view.
Usually, these discussions consider the mere addition of the occurrence of a
competitor or mutualist species as a predictor variable on the model to be
sufficient to account for ecological interactions [@Guisan2006MakBet;
@Wisz2013RolBio; CITATIONS]. Although this practice have demonstrated to improve
the accuracy of distribution models [CITATIONS], the ecological interpretation
is still not convincing. First, as we discussed earlier, the realization of an
interaction is conditional to many factors, including abundance and other
interactions, and it's strength and signal can vary in space and time. Second,
adding a competitor as an equivalent of an absence of the focus species just
informs the model about environmental conditions that are supposedly not
suitable for the establishment of a population, not that an ecological
interaction is taking place there in such a manner that it will influence the
survival of a pair of individuals.  

As reviewed by @Cabral2017MecSim, many models in ecology have considered
competition and facilitation in range shifts, but the assessment of trophic
interactions remains insufficient. An example of good theoretical exercise was
done in @Godsoe2012HowSpe, where authors calculated the probability that a given
site will be environmentally suitable in the presence of a competitor, based on
their population dynamic models [@Godsoe2012HowSpe]. Although it is close to
assuming a binary nature for interactions, it does account for dynamics and
simulate results for different abundances, thus approximating to a probabilistic
approach. There are only a few attempts on the literature that tries to build
mechanistic species distribution models accounting for interspecies interaction
(independent of its nature) as a probabilistic entity [@Cabral2017MecSim]. A
first step in this direction was taken in @Gravel2011TroThe, where authors
demonstrated how interactions can be included in the Theory of Island
Biogeography [@MacArthur1967TheIsl]. This experiment provided a starting framework for
the next generation of species distribution models to include migration dynamics and trophic levels.  

In @Cazelles2016TheSpe, the authors elaborate on @Gravel2011TroThe model and
include environmental constraints in a metacommunities dynamic model in a
biogeographical scale. Their model add some necessary complexity by evaluating
frames of communities in different times, calculating the probability of change
in community composition due to migration, interactions and environmental
requirements. This is a very useful model to understand spatial dynamics of
species richness, and could be used as a validation strategy for HSMs with only
two time frames: the current known distribution and the potential distribution
inferred by the HSM. Because the probability of occurrence of one species is
derived from the probability of occurrence of all other species
[@Cazelles2016TheSpe], we could infer the probability of occurrence of a focus
species based on its potential distribution and local species pools. This
strategy would require to predict interactions between species that did not
previously co-occur.  

In this sense, an interesting approach was elaborated in @Staniczenko2017LinMac,
where the authors address interactions with Bayesian Networks models that update
the probability of occurrence resulted from a HSM. Bayesian Networks (BN) can be
derived from empirical data or inferred from macroecological data, but they
should only represent directional interactions. This was pointed as a limitation
for the use of this workflow, as interactions are often retroactive [CITATION],
but it showed good efficacy when the research subject allows this simplification
[@Staniczenko2017LinMac]. In these networks, the effects of direct and indirect
interactions are spread among the species, and the nodes represent the
probabilities of occurrence. This allows that multiple species are considered at
the same time and to derive the network from the assemblage resulted of a HSM.  

[@Jimenez-Valverde2020DecAbu]

## Take-home messages   

## References
