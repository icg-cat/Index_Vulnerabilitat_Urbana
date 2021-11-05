README
================
09/14/2021

# Presentació i objectius

Aquest document exposa la metodologia seguida per l’elaboració de
l’Índex de Vulnerabilitat Urbana (en endavant IVU) proposat a
Antón-Alonso, Porcel, Cruz i Coll (2020).

S’ha compilat fent servir R 4.0.3 (R Core Team, 2020) i RStudio 1.4.1717
(2020). Les anàlisis pel model basat en *partial least squares path
modeling* (PLS-PM) s’han fet amb el paquet plspm (Sanchez, Trinchera &
Russolillo, 2017). L’organització de la presentació de resultats segueix
les recomanacions de Chin (2010).

El document s’estructura en les següents seccions. La primera secció és
la justificació metodològica del procediment, seguint el raonament
formulat a Antón-Alonso et al. (2020). La segona secció presenta el
model que es sotmet a contrast i el codi utilitat per executar-lo. La
tercera secció presenta els principals resultats. A continuació es
presenta una comparació dels resultats del model per diferents
anualitats. Finalment s’inclou la bibliografia i un annex amb l’output
complet de resultats.

# Justificació metodològica

El text d’aquesta secció prové d’Antón-Alonso et al. (2020).

> (…) a les tècniques d’anàlisi \[utilitzades en la construcció dels
> índex de vulnerabilitat urbana\] hi predominen les estratègies de
> reducció de dimensions (Coombes i Wong, 1994; Pratschke i Haase, 2007,
> 2015), entre les quals l’anàlisi de components principals (ACP) és la
> utilitzada amb una major freqüència. A banda de les seves virtuts, com
> la simplicitat i la interpretabilitat, l’ACP té certes limitacions que
> cal tenir presents (Haase i Pratschke, 2005). D’una banda, l’ACP, com
> l’anàlisi factorial (AF), tracta en conjunt totes les variables, sota
> la premissa que totes tenen relació amb les dimensions subjacents, de
> manera que no permet fer una anàlisi organitzada en dimensions.
> D’altra banda, tant l’ACP com l’AF són estratègies d’extracció de
> variància o covariància, els resultats de les quals són sensibles a
> les particularitats del conjunt de dades i de les variants de la
> tècnica que s’utilitza. Per exemple, en cas que existeixin valors
> atípics, o que s’apliqui algun tipus de rotació als factors, poden
> emergir diferents combinacions de relacions entre les variables i els
> factors. Això dificulta en gran manera la comparabilitat entre
> anualitats, pel fet que no es té certesa que la informació continguda
> en el primer factor de l’anàlisi d’una anualitat es correspongui amb
> la de l’anualitat següent. D’aquí les dificultats que presenta aquest
> mètode per a les anàlisis evolutives i per a la comparativa entre
> territoris. Per superar aquestes limitacions, s’han proposat models
> d’equacions estructurals (Haase i Pratschke, 2005). Aquest mètode
> permet configurar una estructura factorial molt més estable a partir
> del control de les diverses dimensions que agrupen els indicadors que
> intervenen en l’anàlisi (Miles et al., 2016; Pratschke i Haase, 2007,
> 2015), i d’estratègies d’anàlisi per comparar l’estabilitat del model
> al llarg del temps. (…)

> **L’Índex de Vulnerabilitat Urbana (IVU): una proposta per a l’àrea
> metropolitana de Barcelona**

> La proposta d’índex de vulnerabilitat urbana que es presenta en aquest
> article tracta d’atendre les debilitats i mancances metodològiques
> esmentades anteriorment. Es tracta d’una revisió de l’anterior índex
> de vulnerabilitat urbana que ja havien elaborat Antón-Alonso i Porcel
> (2018) per a l’àrea metropolitana de Barcelona a partir d’una ACP i de
> dades censals. El nou Índex de Vulnerabilitat Urbana (IVU) incorpora
> alguns canvis en els indicadors utilitzats i es construeix a través
> d’un model d’equacions estructurals basat en mínims quadrats
> parcials (PLS-SEM), una tècnica d’anàlisi estadística que integra
> estratègies de reducció de dimensions amb l’anàlisi de regressió.
> Aquest mètode permet resoldre les limitacions en l’anàlisi evolutiva
> que s’han explicat anteriorment. A més, per a l’operacionalització del
> model es fan servir majoritàriament dades procedents de registres
> administratius, la qual cosa possibilita que l’índex es pugui calcular
> amb una periodicitat anual.

> \[*PLS-SEM en l’estudi de la vulnerabilitat urbana*\]

> El PLS-SEM permet estudiar les relacions causals complexes entre
> variables manifestes o observades i dimensions latents. El procediment
> permet quantificar la contribució de cada variable manifesta a la seva
> dimensió latent i modelitzar la relació entre les dimensions latents.
> A diferència del vessant dels models d’equacions estructurals basats
> en les covariàncies \[utilitzats per altres autors per l’estudi de la
> vulnerabilitat urbana (com Pratschke i Haase, 2007, 2014)\], la
> tècnica de PLS-SEM permet definir no tan sols models reflectius, sinó
> també models formatius, que són més adients per al tipus d’objecte
> d’anàlisi que aquí s’ha plantejat \[donat el tipus de relació que
> els indicadors mantenen entre ells, així com amb els constructes
> latents\] (Sanchez, 2013).

> Amb l’aplicació d’aquesta tècnica d’anàlisi a l’IVU s’assoleixen
> diversos objectius. En primer lloc, entendre la vulnerabilitat urbana
> com un fenomen complex, en què intervenen diverses dimensions de
> vulnerabilitat. En segon lloc, l’anàlisi proveeix d’una variable
> contínua amb les puntuacions del factor latent resultant, fet que
> possibilita treballar amb la idea de contínuum a partir de la qual es
> concep la vulnerabilitat a l’espai urbà. Finalment, s’aconsegueix
> obtenir uns resultats comparables al llarg de diverses edicions, la
> qual cosa permet fer una anàlisi evolutiva més robusta.

> La construcció del model ha estat guiada per tres principis: a)
> respectar al màxim els elements teòrics; b) aconseguir un resultat tan
> parsimoniós com sigui possible; i c) que aquest sigui fàcilment
> interpretable.

> La definició del model es basa en les aportacions teòriques d’Alguacil
> et al. (2014), segons les quals la vulnerabilitat urbana és el
> resultat de la combinació i retroalimentació de processos d’exclusió
> social i residencial produïts en el territori. Així, es proposen dues
> dimensions, una de risc social i una altra de risc residencial, amb
> tres indicadors cadascuna. La seva confluència en el territori acaba
> definint la vulnerabilitat urbana. A més, també s’introdueixen en el
> model alguns dels efectes que es deriven de la vulnerabilitat urbana,
> com ara les afectacions en el mercat de l’habitatge (preus del
> lloguer), el poc atractiu residencial que presenten aquestes àrees per
> a la població de classe mitjana i els anomenats efectes de barri,
> operacionalitzat a partir dels nivells de formació assolits pels
> residents.

> \[*Fonts de dades i unitats territorials*\]

> La informació a partir de la qual es treballa procedeix de diverses
> fonts de dades, la majoria de les quals alimentades a partir de
> registres administratius: Atles de distribució de renda de les llars,
> Padró municipal d’habitants, Cadastre, Sistema estatal d’Índex de
> Preus de Lloguer d’Habitatge i Cens de població i habitatges. La taula
> 1 mostra l’operacionalització i les fonts d’informació emprades per a
> la construcció de l’IVU.

> Taula 1: Dimensions, conceptes, indicadors i fonts de l’IVU

> Les unitats territorials sobre les quals es calcula l’IVU són els
> anomenats Àmbits Estadístics Metropolitans (AEM) \[veure Mapa 1\],
> unes unitats que s’aproximen al concepte de barri. La delimitació
> d’aquests àmbits ha estat elaborada recentment per l’Àrea de
> Planificació Estratègica de l’Àrea Metropolitana de Barcelona, basada
> en una demarcació prèvia de barris metropolitans realitzada per
> l’IERMB (Antón-Alonso, Cónsola, Donat, Porcel i Coll, 2016). Els AEM
> constitueixen actualment les unitats territorials inframunicipals de
> referència a l’àrea metropolitana de Barcelona i estan conformats per
> 268 unitats que compten amb un mínim de 291 habitants i un màxim de
> 58.180, essent 12.117 la mitjana de població. La no disponibilitat de
> dades directes que informin d’aquestes unitats territorials ha obligat
> a fer servir un mètode d’estimació que es basa en la redistribució de
> la informació procedent de seccions censals o parcel·les residencials
> (en el cas de la informació provinent del Cadastre), per a les quals
> sí que es disposa d’informació. Es tracta d’una estimació inspirada
> en el Cadastral-based Expert Dasymetric System, un dels mètodes areals
> d’interpolació que ja ha estat emprat en altres estudis (Maantay et
> al., 2007; Mora-García i Marti-Ciriquian, 2015).3

> Mapa 1: Àmbits Estadístics Metropolitans

# Model sota contrast

    ##  [1] "OID"            "CODI_AMBIT"     "NOM_AMBIT"      "FREQUENCY"     
    ##  [5] "SUM_Es_Peo"     "SUM_Es_Est"     "SUM_Es_Sol"     "SUM_Es_Ext"    
    ##  [9] "SUM_Es_RBa"     "SUM_Es_RIn"     "SUM_Es_RAl"     "SUM_Es_Atu"    
    ## [13] "SUM_EsPob2"     "SUM_<1900"      "SUM_1900_1954"  "SUM_1955_1975" 
    ## [17] "SUM_>1975"      "SUM_Es_Peo.1"   "SUM_Es_Est.1"   "SUM_Es_Sol.1"  
    ## [21] "SUM_Es_Ext.1"   "SUM_Es_RBa.1"   "SUM_Es_RIn.1"   "SUM_Es_RAl.1"  
    ## [25] "SUM_Es_Atu.1"   "SUM_Es_Mal"     "SUM_Es_Sup"     "SNViv50"       
    ## [29] "%SUM_Viv50"     "Pllog"          "LleiBarrisC"    "LleixPlaBarris"
    ## [33] "P<1900"         "P1900_1954"     "P1955_1975"     "P>1975"        
    ## [37] "Mllar"          "Dens"           "Anys"           "PlaBarrisB"    
    ## [41] "CODI"           "IntPB"

    ##  [1] "OID"            "CODI_AMBIT"     "NOM_AMBIT"      "FREQUENCY"     
    ##  [5] "SUM_Es_Peo"     "SUM_Es_Est"     "SUM_Es_Sol"     "SUM_Es_Ext"    
    ##  [9] "SUM_Es_RBa"     "SUM_Es_RIn"     "SUM_Es_RAl"     "SUM_Es_Atu"    
    ## [13] "SUM_EsPob2"     "SUM_<1900"      "SUM_1900_1954"  "SUM_1955_1975" 
    ## [17] "SUM_>1975"      "SUM_Es_Peo.1"   "SUM_Es_Est.1"   "SUM_Es_Sol.1"  
    ## [21] "SUM_Es_Ext.1"   "SUM_Es_RBa.1"   "SUM_Es_RIn.1"   "SUM_Es_RAl.1"  
    ## [25] "SUM_Es_Atu.1"   "SUM_Es_Mal"     "SUM_Es_Sup"     "SNViv50"       
    ## [29] "%SUM_Viv50"     "Pllog"          "LleiBarrisC"    "LleixPlaBarris"
    ## [33] "P<1900"         "P1900_1954"     "P1955_1975"     "P>1975"        
    ## [37] "Mllar"          "Dens"           "Anys"           "PlaBarrisB"    
    ## [41] "CODI"           "IntPB"          "no_RA"          "antiguitat"    
    ## [45] "Pllog_V0"       "Mllar_V0"

    ## $CODI_AMBIT
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $Anys
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $NOM_AMBIT
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $SOC_estrangers
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $SOC_gentG
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $SOC_baixes
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $ESP_ruinos
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $ESP_antig
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $ESP_dens
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $URB_estudis
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $URB_noRA
    ## 
    ## FALSE 
    ##   804 
    ## 
    ## $URB_lloguer
    ## 
    ## FALSE 
    ##   804

    ##   SOC_estrangers SOC_gentG SOC_baixes ESP_ruinos ESP_antig ESP_dens URB_estudis
    ## 1       39.25741     42.86       45.8      51.08       100 756.4403    51.04396
    ##   URB_noRA URB_lloguer
    ## 1     99.1    362.5916

# Resultats de validació del model

El model proposat es representa gràficament a la Figura 1, i es pot
llegir de la següent manera: *A major vulnerabilitat social i major
vulnerabilitat residencial, major vulnerabilitat urbana*. Es comença
realitzant l’anàlisi sobre les dades d’una anualitat (2017).

**Figura 2: Inner model**

A continuació es presenten els principals resultats pel contrast del
model.

## Measurement model results

Donat que el model plantejat és formatiu, la manera d’avaluar el
measurement model es basarà en les següents mesures:

  - La unidimensionalitat dels constructes (a partir del valor de les
    eigenvalues)
  - Els pesos (weights) i càrregues (loadings) dels indicadors, per
    veure les seves contribucions sobre els constructes latents
  - La multicolinealitat entre els indicadors

Els blocs es poden considerar unidimensionals, ja que en tots tres
casos, la primera eigenvalue és superior a 1 i la segona és inferior a
1. La dimensió residencial seria la que presenta les menors distàncies
entre les eigenvalues i el llindar de referència (1), però en tot cas
els constructes es poden considerar conceptualment diferents. Aquesta
puntuació més baixa estaria relacionada amb el fet que la proporció
d’habitatge en estat ruïnós té un valor molt similar en els
crossloadings de les dimensions Social i Residencial. De manera similar,
la proporció de població major de 75 anys té un loading molt proper però
major a la dimensió Residencial que no a la Social a la qual pertany. La
Figura 2 sintetitza els valors de crossloading.

**Figura 2: Crossloadings**

**Figura 2: Outer model weights**

**Figura 2: Outer model loadings**

Un dels indicadors (població estrangera) té un pes negatiu, però els
loadings són positius (es descarta una codificació inversa). S’observa
una elevada correlació amb la proporció de població amb rendes baixes,
tot i que la correlació entre les dues és inferior al 90% i el VIF
d’aquesta variable és inferior a 5. Per tot plegat, es considerarà
aquest resultat com a no problemàtic. La interpretació seria que la
proporció de població estrangera té una relació negativa amb el
constructe de la vulnerabilitat social, després de controlar per la
proporció de població amb rendes baixes i de gent gran.

**Figura 3: correlacions entre variables manifestes (%)**

**Taula 1: VIF pels indicadors de la dimensió social**

## Structural model

**Figura 4: Inner model**

**Taula 2: Coeficients de regressió per l’Inner model**

**Taula 3: Coeficients de determinació de les variables latents
endògenes**

El valor de la R^2 i de la redundància es poden considerar com a
moderats (l’habilitat dels constructes latents per predir el constructe
endògen és moderada).

**Goodnes of Fit**

### Validació del model via Bootstrapping

A continuació es presenten els resultats del bootstrapping, que és una
estratègia no paramètrica per estimar la precisió dels paràmetres del
PLS.

A cadascuna de les taules a continuació, veiem que les mitjanes
obtingudes per bootstrapping no guarden grans distàncies amb els valors
originals del model, i que els intervals de confiança del 95% no
contenen el 0.

**Taula 4: Bootstrapping weights**

**Taula 5: Bootstrapping loadings**

**Taula 6: Bootstrapping paths**

**Taula 7: Bootstrapping R^2**

**Taula 8: Bootstrapping total effects**

## Anàlisi de les variables latents

La Figura 5 presenta la distribució de les puntuacions obtingudes pels
constructes latents a partir del model.

**Figura 5: Puntuacions de les variables latents**

L’índex de vulnerabilitat urbana té una distribució amb una asimetria
negativa, fent més llarga la cua inferior, el que es pot entendre com un
petit nombre de barris amb un IVU molt baix, que formarien els barris
*menys* vulnerables. Això vol dir que a l’extrem oposat hi ha els barris
més vulnerables, que no formen una cua sinó un bloc. Aquesta mena de
bloc a l’extrem superior s’observa a les tres variables latents.

**Barris a l’extrem superior de cada variable latent**

**Figura 6: Distribució dels barris segons les puntuacions en el
constructe de Vulnerabilitat Urbana i de Vulnerabilitat Social**

**Figura 7: Distribució dels barris segons les puntuacions en el
constructe de Vulnerabilitat Residencial i de Vulnerabilitat Social**

# Resultats d’anàlisi del model

A continuació es presenten un conjunt de mapes on es cartografien els
resultats de l’IVU.

**Mapa 2: Dimensió de la vulnerabilitat residencial. AMB, 2017**

**Mapa 3: Dimensió de la vulnerabilitat social. AMB, 2017**

**Mapa 4: Índex de vulnerabilitat urbana (IVU). AMB, 2017**

# Comparació del model per anualitats

El model exposat fins el moment, realitzat amb dades de 2017, s’aplica a
les dades de 2015 i 2016. A continuació es presenten les anàlisis que
permeten concloure que el IVU de les diferents edicions és comparable.

S’aplica un Two-sample T-test per parells sobre la hipòtesi nul·la que
els dos grups (edicions) són equivalents. L’evidència disponible no
permet rebutjar la H0, per tant podem considerar que els coeficients
dels dos anys són equivalents, o en altres paraules, l’índex és
comparable entre anualitats.

**Figura 8: models IVU 2015 : 2017**

No hi ha diferències entre 2015 i 2016, és a dir, els models es
comporten de manera equivalent i per tant són comparables.

Tampoc hi ha diferències entre 2015 i 2017, pel que també podem dir que
els models són comparables.

# Bibliografia

Antón-Alonso, F., Porcel, S., Cruz, I., Coll, F. (2020). *La
vulenerabilitat urbana a Barcelona: persistència, concentració i
complexitat.* Papers. Regió Metropolitana de Barcelona, 63, pp. 50-67.

Chin, W. (2010). *How to Write Up and Report PLS Analyses*, a Esposito
Vinzi, V., Chin, W.W., Henseler, J., Wang, H. (Eds.). Berlin: Springer.

R Core Team (2020). R: A language and environment for statistical
computing. R Foundation for Statistical Computing, Vienna, Austria. URL
<https://www.R-project.org/>.

RStudio Team (2020). RStudio: Integrated Development for R. RStudio,
PBC, Boston, MA URL <http://www.rstudio.com/>.

Sanchez,G., Trinchera, L. i Russolillo, G. (2017). plspm: Tools for
Partial Least Squares Path Modeling (PLS-PM). R package version 0.4.9.
<https://CRAN.R-project.org/package=plspm>.

# Annex

## Resultats complets del model (2017)
