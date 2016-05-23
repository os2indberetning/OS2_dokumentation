# Code of Conduct for OS2 Indberetning GitHub projekt

Denne beskrivelse udstikker retningslinierne for hvordan aktiviteter i GitHub projektet for OS2 Indberetning skal foregå.

Indhold
<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Strategi for branches og tags - Git Flow](#strategi-for-branches-og-tags-git-flow)
	- [Brug et værktøj](#brug-et-vrktj)
	- [Git Flow basale dele](#git-flow-basale-dele)
	- [Git Flow på GitHub](#git-flow-p-github)
- [Release, herunder nummerering](#release-herunder-nummerering)
	- [Nummerering af releases](#nummerering-af-releases)
	- [Beta og test releases](#beta-og-test-releases)
- [Håndtering og rollefordeling ved Pull Requests (PR)](#hndtering-og-rollefordeling-ved-pull-requests-pr)
- [Rapportering af fejl og mangler og processer omkring dette](#rapportering-af-fejl-og-mangler-og-processer-omkring-dette)
- [Forløb af større udviklingsprojekter af moduler og udvidelser](#forlb-af-strre-udviklingsprojekter-af-moduler-og-udvidelser)

<!-- /TOC -->

## Strategi for branches og tags - Git Flow

I dette projekt skal metoden Git Flow benyttes. Den er beskrevet her:

    http://nvie.com/posts/a-successful-git-branching-model

og her

    http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/

### Brug et værktøj

Det anbefales kraftigt at bruge et værktøj der understøtter git flow. Til kommandolinien kan denne benyttes

    https://github.com/nvie/gitflow

Hvis et GUI tool ønskes kan SourceTree (gratis) anbefales

https://www.sourcetreeapp.com

### Git Flow basale dele

Når Git Flow følges er der 2 git branches der lever hele tiden:
* develop - løbende udvikling
* master - ét commit per release

Der committes aldrig direkte på master branch men kun som et resultat af et trin git flow.

**Feature branches**

Som udgangspunkt oprettes til hver bid udvikling en såkaldt feature-branch. Selvom navnet kunne antyde andet bruges dette også til almindelige (ikke-panik) fejlrettelse og altså til alt udvikling inden for projektet.

En feature branch hedder altid "feature/**navn**" hvor **navn** er et beskrivende navn for denne feature. Det er fint hvis **navn** indeholder f.eks. Jira issue navn men det er nødvendigt at det også indeholder andet. Stammer det fra et Jira issue kan dette issues summary passende bruges.

Når feature branches altid starter med "feature" efterfulgt af en slash "/" vil det optræde som en folder (directory).

Når en feature afsluttes og dermed merges ind i develop *skal* den tilhørende branch slettes. Intet går tabt ved denne sletning ud over dens navn.

**Release branches**

Som en del af git flow kan der benyttes release branches til at færdiggøre en release uden at forstyrre develop branchen. Typisk er dette dog ikke strengt nødvendigt men git flow værktøjer vil lave en alligevel men den ender med at være tom og blive slettet igen i næste trin af værktøjet.

**git tags**

Endhver release lavet igennem git flow resulterer i en tag i git og denne tag tilhører en commit på master branch. Det *skal* derfor også være dette kode der bruges som udgangspunkt for build til release.

### Git Flow på GitHub

Det er vigtigt at være opmærksom på at bruges et værktøj såsom SourceTree til at lave git flow, vil værktøjet automatisk merge en feature branch ind på develop når man beder den om at "finish" en feature.

Dette er ikke altid den ønskede fremgangsmåde hvis udvikler af denne feature ikke er en del af Gatekeeper gruppen / organisationen.

I sådan et tilfælde er det bedre *ikke* at bruge værktøjet til at "finish" feature men derimod gå ind på GitHub.com og lave en pull request (PR).

Herved bliver Gatekeeper indvolveret og kan sørge for de rette procedurer for at merge denne feature ind i develop.

Dette er også tilfældet hvis udvikler slet ikke har commit adgang til OS2 Indberetning GitHub projekt og derfor har måttet lave en fork på GitHub.

Se iøvrigt afsnittet [Håndtering og rollefordeling ved Pull Requests (PR)](#hndtering-og-rollefordeling-ved-pull-requests-pr) herunder.

## Release, herunder nummerering

Alt software der sendes til test eller i produktion *skal* igennem et git flow release forløb. Hvis det er til test kan der laves en beta release.

### Nummerering af releases

Der benyttes såkaldt Semantic Versioning.

    http://semver.org

Det betyder at alle releases som minimum vil have et nummer i 3 dele adskildt af punktum.
* Første del er "major" og øges når større ændringer indføres
* Anden del er "minor" og øges når mindre og bagudkompatible ændringer indføres.
* Sidste del er "path" og kan bruges til rene fejlrettelser, dvs. ingen nye features

Alle releases der giver nye features skal således øge minor eller major delen, alt efter om API'en ændres. Da de mobile apps releases separat fra serverdelen vil API her også skulle forståes som ikke kompatible ændringer i kommunikationen imellem server og mobile klienter.

Et release nummer kan således f.eks se således ud:
* 2.7.5

Der er ingen begrænsning på størrelse af tallet i de tre dele.

### Beta og test releases

Når softwared skal sendes til test, installeres i testmiljø synligt for brugere eller på anden måde præsenteres for brugere, interessanter eller QA, *skal* der laves en release. Sådanne releases kan navngives så det er tydeligt at det er en beta release.

Dette gøres ved at tilføje "-beta.nummer" til release navnet, f.eks.
* 2.7.5-beta.4

I dette eksempel vil dette være en test release som leder op til den endelige 2.7.5 release.

Når først release 2.7.5 er lavet kan der ikke laves flere beta releases til denne. Opdages en fejl kan der så f.eks. udsendes en beta release kaldet 2.7.6-beta.1


## Håndtering og rollefordeling ved Pull Requests (PR)

Når en udvilker ønsker en ændring merged ind i develop branchen laves en pull request på GitHub, enten fra en feature branch i OS2 Indberetning GitHub projektet eller fra en fork af dette.

Når en pull request bliver lavet vil Gatekeeper automatisk blive underrettet. Gatekeeper vil så gennemløbe følgende process:
* Analyser PR for indhold og formål
* Lav en vurdering af omfang for integration og test efterfølgende
* Lav en vurdering af indflydelse og risiko ved ændringen
* Forelæg PR og vurderinger for styregruppen
* Mulige beslutninger fra styregruppen kan være
  - Integration
  - Modificer PR således nye dele kan konfigureres væk
  - Afvis som uønsket, evt. med forslag til hvad der kan ændres for at gøre PR ønsket
* Integration af PR i develop hvis det er beslutningen fra styregruppen
* Test
* Release der indeholder PR, hvis det et beslutningen fra styregruppen

## Rapportering af fejl og mangler og processer omkring dette

Deciderede fejl og mangler skal indrapporteres til Gatekeeper direkte. Udvalgte brugere har adgang til denne kommunikationskanal.

Når en fejlrapport er lavet vil Gatekeeper gennemløbe følgende process
* Analyser fejlrapport for validitet, indhold og omfang af konsekvenser
* Lav en vurdering af omgang for at løse fejl og teste efterfølgende
* Forelæg fejlrapport og vurderinger for styregruppen
* Mulige beslutninger fra styregruppen kan være
    - Ret fejl som beskrevet
    - Delvis afvirkning af symptomer vha andre tiltag eller rettelser
    - Afvis, evt. med forslag til hvad der skal beskrives yderligere ved fejlen
* Ret fejl i develop hvis det er beslutningen fra styregruppen
* Test
* Release der indeholder fejlrettelse, hvis det et beslutningen fra styregruppen

## Forløb af større udviklingsprojekter af moduler og udvidelser

Større udviklinksprojekter af moduler og udvidelser skal foregå vha GitHub's mulighed for at lave et "fork" af OS2Indberetning projektet.

På denne fork skal der skal der stadig arbejdes med branches, gerne ifølge Git Flow.

Når et udviklingsprojekt er nået til en milepæl eller er færdigt, skal der laves en pull-request fra en branch på udviklingsprojektets fork, tilbage til develop branchen på OS2Indberetning.

Denne pull-request vil så blive behandlet af Gatekeeper som beskrevet ovenfor under "Håndtering og rollefordeling ved Pull Requests (PR)".
