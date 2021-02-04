Përshkrimi i problemit
Projekti ka për qëllim krijimin e një programi në C në Linux që përdor multithreading përmes POSIX thread-ave duke përdorur disa nga funksionet (rutinat) e tij. Funksionet që janë përdorur janë: pthread_create, pthread_exit, pthread_cancel, pthread_attr_init dhe pthread_attr_destroy, si dhe funksioni pthread_join. 
Sot, multithreading është teknologji softueri i cili është mandator për platformat kompjuterike moderne të çfarëdo lloji dhe gjithashtu një kuptim i qartë për rolin e përgjithshëm dhe ndikimin e thread-ave. 
Problemi i trajtuar në këtë projekt zgjidhet në mënyrë shumë të lehtë me anë të multithreading përkatësisht përmes POSIX thread-ave. 
Problemi që ne kemi trajtuar në kuadër të këtij projekti është krijimi i një programi i cili krijon dy thread-a të cilët përmbajnë në kuadër të tyre nga një metodë përkatëse (njëri për gjenerimin e një fjale dhe tjetri për gjenerimin e një numri të rastësishëm). Zgjidhja e problemit është funksionale dhe është arritur përdorimi i secilit funksion në program.
Ekzekutimi i programit bëhet përmes terminalit duke dhënë komandat përkatëse të cilat i shohim në pjesët e mëposhtme.
Më poshtë kemi treguar teknologjinë që kemi përdorur për këtë projekt dhe se çfarë bëjnë secili funksion (rutinë) i kërkuar për zgjidhjen e problemit.

Teknologjia 
Për zgjidhjen e problemit ne kemi përdorur:
-	Editorin: gedit;
-	Sistemin Operativ: Ubuntu;
-	Gjuhën programuese: C.

Konceptet bazë
Koncepti i multi-threading  kërkon kuptimin e duhur të  dy termave : proces dhe thread. 
Një proces është një program që ekzekutohet, ku mund të ndahet më tej në njësi të pavarura të njohura si thread.
Një thread është si një proces i vogël me peshë të lehtë brenda një procesi ose mund të themi se një koleksion (bashkim) thread-ash është ai që njihet si proces.
Multithreading është aftësia e një programi ose një procesi të sistemit operativ për të menaxhuar përdorimin e tij nga më shumë se një përdorues në të njëjtën kohë dhe madje për të menaxhuar kërkesa të shumta nga i njëjti përdorues pa pasur nevojë të ketë shumë kopje të programimit që ekzekutohet në kompjuter. Çdo kërkesë e përdoruesit për një program ose shërbim të sistemit (ku këtu një përdorues mund të jetë edhe një program tjetër) mbahet si një thread me një identitet të veçantë. 

POSIX Threads, zakonisht të referuara si pthreads, është një model ekzekutimi që ekziston në mënyrë të pavarur nga një gjuhë, si dhe një model ekzekutimi paralel. Ai lejon një program të kontrollojë flukse të ndryshme të punës që mbivendosen në kohë (overlap in time). Çdo rrjedhë e punës referohet si një thread, dhe krijimi,kontrolli mbi këto rrjedha arrihet duke bërë thirrje në API-në e POSIX Threads. POSIX thread është një API i përcaktuar nga standardi POSIX.1c, Threads extensions (IEEE Std 1003.1c-1995).
Funksioni pthread_create
PËRSHKRIMI :
Funksioni pthread_create përdoret për të krijuar një thread të ri, me atributet e specifikuara nga attr, brenda një procesi. Nëse attr është NULL, përdoren atributet e paracaktuara (default). Nëse atributet e specifikuara nga attr modifikohen më vonë, atributet e thread-ave nuk afektohen. Pas përfundimit të suksesshëm, pthread_create ruan ID-në e thread-it të krijuar në vendin e referuar nga thread-i.
Nëse pthread_create dështon, nuk krijohet thread-i dhe përmbajtja e vendndodhjes së referuar nga thread nuk përcaktohet.

PARAMETRAT:
thread
          	Është vendndodhja ku duhet të ruhet ID-ja e thread-it të sapo krijuar, ose mund të jetë NULL
          	nëse ID-ja e thread-it nuk kërkohet.
attr   	
         	Është objekti i atributit të thread-it që specifikon atributet për thread-in që po krijohet. Nëse attr
         	është NULL, thread-i krijohet me atribute të paracaktuara (default).
start
         	Është funksioni kryesor për thread-in. Thread-i fillon ekzekutimin e kodit në këtë adresë.
arg
         	Është argumenti që kalohet për të filluar krijimin e thread-it. 
VLERA KTHYESE:
Nëse është i suksesshëm, funksioni  pthread_create () kthen zero. Përndryshe, kthehet një numër gabimi për të treguar gabimin. 
ERROR-AT:
Funksioni pthread_create do të dështojë nëse:

[EAGAIN] shfaqet kur performojmë me I/O jo-bllokuese. Kjo do të thotë "nuk ka të dhëna të disponueshme tani, provo përsëri më vonë".
●	Sistemit i mungojnë burimet e nevojshme për të krijuar një thread tjetër.

[EINVAL] tregon që një (ose më shumë) parametra kanë vlera të pakuptimta.
●	Vlera e specifikuar nga attr është e pavlefshme. Pra, attr nuk është një objekt i atributit fillestar të thread-it.

[EFAULT] Ndodh nëse adresa e memories e disa argumenteve të kaluara është e pavlefshme.
Nëse thread-i ose attr është një pointer i pavlefshëm.

Funksioni pthread_exit

PËRSHKRIMI : 
Funksioni pthread_exit ka dy role të ndryshme. Nëse përdoret në main thread, e bën atë të presë derisa të gjitha user level threads të terminojë. Nëse përdoret në një thread funksion, do të funksionojë si një exit call. Pthread_exit do të përfundojë thread-in që është thirrur. Nëse e thërrasim atë nga main thread, main thread mbaron dhe thread-i jonë vazhdon ekzekutimin. Kështu që gjithçka që shkruajmë pas pthread_exit në fijen kryesore nuk do të ekzekutohet. 
Nëse shkruajmë dalje ose kthim në main thread, i gjithë procesi përfundon, por nëse shkruajmë pthread_exit në main thread vetëm thread-at e veçantë përfundojnë dhe thread-at e mbetur vazhdojnë ekzekutimin e tyre.

PARAMETRAT:
status
                 është exit status për thread 
VLERA KTHYESE:
Funksioni ptherad_exit nuk mund të kthejë return tek caller i tij.
ERROR-AT:
Error-at nuk janë të definuar.
Funksioni pthread_cancel
PËRSHKRIMI : 
Funksioni pthread_cancel kthehet pasi të bëjmë kërkesën. Veprimi i anulimit në targetin e synuar ekzekutohet asinkronikisht në lidhje me thread-in e thirrur duke u kthyer nga pthread_cancel. Thread-i i targetuar  anulohet bazuar në aftësinë e saj për t'u anuluar.
Kur aftësia e anulimit është çaktivizuar, të gjitha anulimet mbahen pezull në thread-in e synuar derisa thread-i të ndryshojë aftësinë e anulimit. Kur anulimi shtyhet, të gjitha anulimet mbahen pezull në thread-in  e synuar derisa thread-i të ndryshojë aftësinë e anulimit, thirrjen e një funksioni që është një pikë anulimi ose thirrjet.

PARAMETRAT:
thread 
                thread-i i cili do të anulohet.
VLERA KTHYESE:
Nëse ka sukses kthen 0 .
Nëse ka error kthen një nga vlerat e mëposhtme:
[ESRCH]: thread-i nuk specifikon një thread që është duke u ekzekutuar.
Funksioni pthread_attr_init
PËRSHKRIMI : 
Funksioni pthread_attr_init() e inicializon një objekt attr të atributeve të thread-it, me vlerën default për të gjitha atributet individuale të përdorura gjatë një implementimi.
Objekti përfundimtar i atributit (ka mundësi që është ndryshuar, duke ju vendosur vlera atributeve individuale), gjatë përdorimit nga pthread_create, definon atributet e thread-it të krijuar. Një objekt i vetëm i atributeve mund të përdoret njëkohësisht në shumë thirrje të pthread_create. Thirrja e pthread_attr_init në një objekt të atributeve të thread-it që është inicializuar më hëret, rezulton në një sjellje të padefinuar (undefined behavior).
VLERA KTHYESE:
Pas ekzekutimit të suksesshëm, pthread_attr_init kthejnë vlerën 0 ,përndryshe, një id e error-it do të kthehet për të treguar errorin e hasur.
ERROR-AT:
Funksioni pthread_attr_init do të dështojë nëse:
 [ENONEM]
●	 Nuk ka memorie te mjaftueshme për të inicualizuar objektin e atributeve të thread-it
            	Ky funksion nuk do të kthejë një kod errori [EINTR].

Funksioni pthread_attr_destroy
PËRSHKRIMI : 
Shkatërron një objekt të atributeve të thread-ëve dhe nuk ka asnjë efekt në thread-at që janë krijuar duke përdorur atë objekt.

PARAMETRAT:
attr 
         është objekt atributi i thread-it.
VLERA KTHYESE:
Nëse ka sukses pthread_attr_destroy kthen 0.
Nëse ka gabim kthen njërën ngaa vlerat e mëposhtme:
[EFAULT] - attr është një pointer invalid.
[EINVAL] - attr nuk referohet për të inicializuar objekt atributin e thread-it.
ERROR-AT:
Errorat nuk janë të definuar.

Funksioni pthread_join
PËRSHKRIMI       
Funksioni pthread_join pret që thread-i i specifikuar të terminohet. Nëse ai thread nuk ka terminuar ende pthread_join kthehet menjëherë. Nëse shumë thread-a njëkohësisht provojnë të bashkohen (join), rezultatet janë të padefinuara.
VLERA KTHYESE
       Në ekzekutim të suksesshëm, pthread_join kthen 0; nëse ka error, kthen një numër error-i.
ERROR-AT
       [EDEADLK]
●	   Është vërejtur një deadlock (p.sh. dy thread-a kanë provuar të bashkohen me njëri-tjetrin); ose thread-i specifikon thread-in e thirrur.
      [EINVAL] - thread-i nuk është një joinable thread.
      [EINVAL] - një thread tjetër tashmë po pret të bëhet join me atë thread .
      [ESRCH] - nuk mund të gjendet ndonjë thread me ID e specifikuar.
Disa nga përfitimet e MultiThreading
●	Përgjegjësia. Rrit përgjegjësin ndaj user-it pasi lejon programin të vazhdojë ekzekutimin edhe nëse një pjesë e tij po kryen një operacion të gjatë ose është i bllokuar për ndonjë arsye.
●	Ndarja e burimeve. Kjo i lejon thread-ave të ndajnë burime si të dhëna, memorie, fajlla etj. Prandaj, një aplikacion mund të ketë shumë thread-a brenda të njëjtës hapësirë adrese. Pra, lejon shfrytëzimin më të mirë të burimeve.
●	Ekonomia. Krijimi dhe menaxhimi i fijeve ështe më i lehtë dhe merr me pak kohë sepse ato ndajnë  burimet e njëjta të procesorit.
●	Scalability. Një thread ekzekutohet në një CPU. Në proceset me shumë thread-a, thread-at mund të shpërndahen në një seri procesorësh për t'u shkallëzuar.

Në aspektin e  dizajnit, multithreading siguron qëndrueshmëri në softuer. Ai shmang rrënimin e sistemit duke trajtuar secilin thread si një njësi të pavarur dhe duke maskuar defektet në performancën e një thread që afekton të tjerët.

Përfundim

Nga i gjithë ky projekt ne mund të përfundojmë se pthreads (POSIX thread-at) janë më efiçiente pasiqë për menaxhimin e tyre duhen pak resurse dhe poashtu rrit performancën e sistemit operativ.
Përvoja bazë që kemi fituar nga ky projekt është njohja më nga afër dhe më e thellë e procesit të multithreading përmes POSIX thread-ave dhe rolin që ka.
Ne mendojmë se kërkesat e projektit janë realizuar me sukses duke filluar nga përdorimi i rutinave të kërkuara e deri tek funksionaliteti i programit.
