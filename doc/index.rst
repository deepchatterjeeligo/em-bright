.. ligo.em-bright documentation master file, created by
   sphinx-quickstart on Aug 7, 2023.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Documentation of EM-Bright
==========================

Introduction:
-------------
Binary system of neutron stars and black holes are some of the strongest
and best understood emitters of gravitational waves. Additionally, when 
a system has a neutron star then there is also a finite probability of 
disrupted baryonic matter present after the coalescence. This disrupted 
matter could be either from physical collision of the two compact objects
as in the case of a binary neutron star (BNS), or from tidal interactions
between the two compact objects with at least one of them being a neutron
star (NS). This baryonic matter is generally extremely neutron rich, and
will undergo r-process neucleosynthesis producing heavy elements that 
subsequently goes through nuclear fission, producing large quantity of
energy. This may result in an electromagnetic signal, commonly known as
a Kilonova. Simultaneous observation of Kilonova and gravitational wave
resulting from the coalescence of the gravitational wave is one of the 
most sought after astrophysical transient phenomenon. However, these
events are much rapidly evolving than supernova, and the localization
region of gravitational wave can be several tens of square degree in size. 
Thus, early knowledge about the possibility of an electromagnetic 
counterpart of a gravitational wave event can be helpful for observers.

Similarly, another interesting astrophysical event would be the binary coalesence 
of compact objects in the "mass gap" region. Stellar evolution models predict 
that black holes with masses in two ranges cannot be directly formed by the 
gravitational collapse of a star. These mass ranges are distinguished as the 
"lower" and "upper" mass gaps. The lower mass gap is traditionally considered 
to be in mass range fom 3 to 5 M_{\odot}.  Astronomers may be interested in following 
up gravitational-wave sources whose component masses lie in this "lower mass-gap" 
region between neutron stars and black holes.

The EM-Bright package provides tools for computing a machine learning based 
score for the potential presence of an electromagnetic counterpart and the presence of a 
mass gap object in a merger of two compact binary objects. For a given compact
binary coalescence event the EM-Bright code provides three scores, **HasNS**, 
**HasRemnant** and **HasMassGap**. The first quantity gives a score for 
the presence of a neutron star in the binary. The second quantity is the score of 
non-zero tidally disrupted matter to be present outside the final object after 
coalescence. Both these quantities are EoS maginalized. In the case of a neutron star -black hole 
we use a fitting formula of numerical relativity results as provided in Foucart_. The third 
quantity gives the score to quantify whether the binary system has at least one compact 
object which lies in the lower mass gap region.


EM-Bright Calculation:
----------------------
The knowledge of the masses and spins of the binary will allow us to compute the **HasNS**
, **HasRemnant**, and **HasMassGap** scores. However, the source parameter information are 
poorly known in the low-latency, it might be hours before we get the first results from rapid
parameter estimation to directly compute the EM-Bright scores. To address
this issue, we implement a supervised learning technique to compute **HasNS** and 
**HasRemnant** EMBright-paper_. In its current implementation we apply a nearest neighbor
supervised learning technique to train the classifier based on a large set of simulations.
Similary, we compute **HasMassGap** using a supervised learning technique, Random Forest, 
trained on a similarly large set of simulations.

In this study we inject compact binary coalescence signals in noise stream of LIGO and 
Virgo detectors. We recover these injections using the detection pipelines used by the
LIGO/Virgo collaboration. The recovered parameters exhibit deviation from the injected
parameters due to pipeline systematics. We train the classifier to identify the "true"
nature of the event based on the injected parameters where the feature set is the recovered 
parameters. 



.. _Foucart: https://arxiv.org/abs/1807.00011
.. _EMBright-paper: https://arxiv.org/abs/1911.00116


.. toctree::
   :maxdepth: 1
   :caption: Contents:

   Installation
   em_bright
   compute_disk_mass
   release
   O3_MDC



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
