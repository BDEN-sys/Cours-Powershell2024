# Powershell



## Introduction et historique


### Utilité d'un script ?
* Évite les tâches d'administration répétitives et fastidieuses. (Par ex. : création de comptes)
* Améliore la qualité des données du SI en évitant la double saisie d'informations.
* Standardisation des procédures.


### Un peu d'histoire

* Chez Microsoft, DOS v1.0 arrivera en 1981 et permettra d'exécuter des scripts Batch.
* En 1987, PERL (Practical Extraction and Report Language) est développé pour faciliter la manipulation de fichiers et de données. Ne sera disponible sous Windows qu'en 1997. (NT4.0)
* Javascript arrive avec Netscape et Jscript avec Internet Explorer 3.0.
* Le kit de ressource Microsoft Technique permet d'utiliser PERL et Kickstart avec NT4.0
* Avec l'arrivée de Windows 98 et l'Option Pack NT 4.0 arrive l'environnement WSH (Windows Scripting Host). Celui-ci permet l'exécution de scripts VBScripts.


* En 2004, 2005 : Prise de conscience de Microsoft des limites de l'interface graphique. (Environnement d'exécution de scripts très limité par rapport à d'autres systèmes)
Le projet Monad puis PowerShell v1 arrive en 2006.
* En 2009, sortie de PowerShell v2 intégré à Windows 7/2008R2.
* Nouvelle stratégie Microsoft orientée vers la ligne de commande : Exchange 2007-2010, Windows 2008 R2, MDT, SQL Server 2008... et autres sociétés comme VMWARE (PowerCLI), Citrix Xen APP,...
* En 2012, sortie de PowerShell v3 intégré à Windows 8/2012.
* En 2013, sortie de PowerShell v4 intégré à Windows 8.1/2012R2
* En 2014, sortie de PowerShell v5 intégré à Windows 10.
* En 2016, sortie de Powershell v5.1
* En 2018, sortie de PowerShell Core 6.0 (Linux et OSX)
* En 2020, sortie de PowerShell 7 (version LTS)
* Fin 2023, dernière version LTS - Powershell V7.4



## Les bases


### Présentation de Powershell

* Powershell est un interpréteur de commandes tel que "CMD.EXE" ou un shell Linux (sh, bash...)
* Il s'appuie sur le framework .NET, et permet d'utiliser des objets.
* PS v2.0 ==> 260 commandes, v3.0 ==> 350 commandes, 
* Noms des commandes faciles à mémoriser, car toujours basés sur le même modèle.
* Aide en ligne intégrée à la console très détaillée.

> Le framework .NET, est un ensemble de composants constitué d'un moteur d'exécution et d'une bibliothèque de classes à partir desquelles nous pouvons instancier des objets. 
<!---### Prérequis Powershell v2.0

* Windows 7 / Windows Server 2008 R2 : PowerShell 2.0 est prêt à l'emploi
* Windows Vista SP1 minimum : Binaires PowerShell x86 ou x64
* Windows Server 2008 : Binaires PowerShell x86 ou x64
* Windows Server 2003 SP2 ou 2003 R2 : Binaires PowerShell x86 ou x64 + Framework .NET 2.0 SP1 (minimum)
* Windows XP SP3 : Binaires PowerShell x86 + Framework .NET 2.0 SP1 (minimum)
* Windows 2000 : Non disponible-->


### Prérequis Windows Powershell 5.1

* Natif sur Windows Server 2016 et Windows 10/11
* Pour les anciens systèmes : installation de Windows Management Framework (WMF) 5.1 :
  * OS clients : Windows 7 SP1 et Windows 8
  * OS serveurs : Windows Server 2008 R2 SP1 et Windows Server 2012 et R2

* Windows Management Framework (WMF) 5.1 :
  * Contient un ensemble de programmes : PowerShell 5.1, WMI, WinRM, Windows PowerShell Desired State Configuration.  
  * Disponible à cette adresse : [Windows Management Framework (WMF) 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)


### Prérequis Powershell 7 

* Compatible à partir de Windows 10 et Windows Server 2016


### Généralités Powershell

* Les fichiers exécutables **powershell.exe** et **pwsh.exe** sonts installés dans les répertoires suivants :

  * `C:\Windows\System32\WindowsPowerShell\v1.0 (Windows Powershell)`
  * `C:\Program Files\PowerShell\7 (Powershell 7)`

* WinRM et WSMan sont nécessaires pour l'exécution de scripts à distance et en arrière plan.


### Quelques éditeurs avec colorations syntaxiques

#### ISE - Integrated Scripting Environment

* L'éditeur **ISE** est disponible dans Windows 2008 R2/7/8/10/11. Il propose entre autres ces fonctionnalités :
  * Édition multiligne
  * Exécution sélective
  * Aide contextuel
  * Console d'exécution (Windows Powershell)
  * Panneau de commandes avec filtre
  * Auto-Complétion
  * Affichage des erreurs de syntaxe
  


#### VSCODE - Integrated Scripting Environment

* L'éditeur **VSCODE** est utilisable avec MacOSX, Linux et Windows.
  * Intégration de la console PowerShell (Windows Powershell et Powershell 7)
  * Extension PowerShell (autocomplétion, coloration syntaxique et le débogage)
  * Débogage avancé (points d'arrêt, inspection des variables et suivi de  l'exécution des scripts pas à pas)
  * Gestion par dossier/projet (explorateur intégré)
  * Suivi des modification (intégration de GIT via une extension)


### Commandes pour débuter

Les commandes (cmdlets) natives de PowerShell sont constituées d'un verbe + un nom.
Bien que les noms des commandes soient plus longs, elles sont plus facilement mémorisables.

* Exemples de verbe : Get, New, Set, Clear, Import, Set, Write ...
* Exemple de noms : Content, Item, Host, ChildItem ... 

```powershell
    # Obtenir toute la liste des commandes natives ou installées via modules
    Get-Command -CommandType cmdlet
    # Nombre de commandes Powershell :
    Get-Command -CommandType cmdlet | Measure-Object
    Count : 236
```


* Obtenir les commandes commençant par "Get-"

```powershell
Get-Command Get-*
CommandType Name        Definition
———–        —       ———
Cmdlet      Get-Acl     Get-Acl [[-Path] &lt;String[]>] [-Audit]...
Cmdlet      Get-Alias       Get-Alias [[-Name] &lt;String[]>]...
Cmdlet      Get-Authenticode... Get-AuthenticodeSignature [-FilePath]...
...
```

* Commandes s'appliquant à item :

```powershell
Get-Command *-item
CommandType Name        Definition
———–        —           ———
Cmdlet      Clear-Item  Clear-Item [-Path] &lt;String[]> [-Force] [-Filter ...
Cmdlet      Copy-Item   Copy-Item [-Path] &lt;String[]> [[-Destination]..
...
```


* Obtenir de l'aide avec la commande Get-Help :
```powershell
Get-Help maCommande
Help maCommande
maCommande - ?
```
* Il existe plusieurs niveaux d'aide :

    * l'aide standard :
    ```powershell
    Get-Help maCommande
    ```
    * l'aide détaillée
    ```powershell
    Get-Help maCommande -detailed
    ```
    * l'aide complète :
    ```powershell
    Get-Help maCommande -full
  


* L'utilisation de la commande Help affiche l'aide page par page.
* Help est une fonction qui passe le contenu de Get-Help à more.
* Help utilisé sans argument, affiche toutes les rubriques d'aide de Powershell.

> Help about_* affiche les rubriques d'aides concernant les tableaux, les opérateurs de comparaison, les boucles, les fonctions,...


* La commande Get-Member liste toutes les propriétés et méthodes d'un objet ainsi que son type.
```powershell
    $TestVariable = 'Hello Word !'
    $TestVariable | Get-Member  
 
    TypeName : SystemString  
    
    Name      MemberType Definition
    ———–      —           ———
    Clone     Method     System.Object Clone()
    CompareTo Method     int CompareTo (System.Object valu...
    ....
    ToUpper   Method     String ToUpper(), string ToUpper...
    ToLower   Method     String ToLower(), string ToLower...
    ....
    Length    Property   System.Int32 Length get ;
```  

* Le résultat nous donne deux types d'informations :
    * Le champ TypeName avant le tableau indique le type de la variable.
    * La liste des méthodes et propriétés de la variable.


* Exemple avec les méthodes ToUpper() et ToLower()

```powershell
    $TestVariable.ToUpper()
 
    HELLO WORLD !

    $TestVariable.ToLower()
 
    hello world !
```

* Exemple avec la propriété Length
```powershell
    $TestVariable.Length
 
    13
```



## Utilisation du shell


### Commandes CMD et Shell Linux

* Anciennes commande Windows (cmd.exe) sous forme d'alias :
    ```powershell
    dir,md, cd, rd, move, ren, cls, copy
    ```
* Et aussi pour les Unixiens :
    ```powershell
    ls, mkdir, cp, mv, pwd, cat, mount, lp, ps
    ```
* Ces anciennes commandes sont des alias prédéfinis qui se substituent aux commandes natives.

    > Pour visualiser les alias : **get-alias** 


* Exemple avec la commande dir :
```powershell
    dir

    Mode LastWriteTime      Length Name
    —    ————               ——     —
    d—   09/02/2012 23:10          XML
```
    
* Correspondance alias dir et commande native :
```powershell
    Get-Alias dir
    
    CommandType Name Definition
    ———–        —    ———
    Alias       dir  Get-ChildItem
```


* Correspondance alias "Windows" et commandes natives :
```powershell
    Get-Alias dir,md,cd,rd,move,ren,cls,copy
     
    CommandType Name    Definition
    ———–        —       ———
    Alias       dir     Get-ChildItem
    Alias       md      mkdir
    Alias       cd      Set-Location
    Alias       rd      Remove-Item
    Alias       move    Move-Item
    Alias       ren     Rename-Item
    Alias       cls     Clear-Host
    Alias       copy    Copy-Item
```

> **md** est l'alias de **mkdir** qui n'est pas une commande native mais une **fonction** utilisant la commande native set-item.


* Correspondance alias "Unix" et commandes natives :
```powershell
    Get-Alias ls,mv,pwd,mount,cp,ps
    
    CommandType Name    Definition
    ———–        —       ———
    Alias       ls      Get-ChildItem
    Alias       mv      Move-Item
    Alias       pwd     Get-Location
    Alias       mount   New-PSdrive
    Alias       cp      Copy-Item
    Alias       ps      Get-Process

```


### Lister des fichiers/répertoires

* Get-Childitem (gci, dir, ls)

```powershell    
    gci c:\
     
    Répertoire : C:\
    Mode LastWriteTime Length Name
    ---- ------------- ------ ----
    d-r-- 29/01/2012 22:45 Program Files
    d-r-- 29/01/2012 21:49 Users
    d---- 30/01/2012 15:37 Windows
    -a--- 11/02/2012 21:32 6 autoexec.bat
    	
    Colonne Mode :
    d : répertoire
    a : archive
    r : lecture seule
    h : fichier caché
    s : fichier système
```

* Pour afficher les fichiers cachés : 

```powershell 
    Get-Childitem -force 
```


* Lister de manière récursive

```powershell
Get-ChildItem c:\temp\* -Recurse
```

* Lister tous les fichiers supérieurs à 640 Mo :

```powershell
Get-ChildItem | 
Where-Object {$_.Length -gt 640MB}
```

* Lister tous les fichiers enregistrés avant le 1 janvier 2018

```powershell
Get-ChildItem |
Where-Object {$_.LastWriteTime -lt '01/01/2018'}
```

> **Notions d'objets :**  
Les deux exemples précédents montrent que Powershell utilise des objets. En effet l'objet est transféré par le pipe vers la commande Where-Object qui filtre sur la propriété spécifiée. 


## Se déplacer dans le système de fichiers

* Set-Location (sl,cd)

    ```powershell
    Set-Location F:\
    ```

* Utilisation de chemins relatifs :

    ```powershell
    Set-Location ..
    Set-Location /
    ```

> **cd..**  
Depuis l'antique DOS, il était possible d'utiliser cd.. sans espace entre les deux points et cd. Ce n'est plus disponible dans PowerShell V1 mais de retour dans la version 2. 


* Se repérer dans l'arborescence de fichiers : Get-Location (gl,pwd)
```powershell
    Get-Location
    
    Path
    -------
    D:\scripts
 ```
* Récupérer le chemin courant dans une variable :
```powershell
    $chemin = (Get-Location).Path
    $chemin
    
    D:\scripts
```


## Création de dossiers et de fichiers

* New-Item (ni, md)

* Créer un nouveau dossier :

```powershell
    New-Item -ItemType directory -Name 'Nouveau Dossier'
    #Ou
    mkdir 'Nouveau Dossier'
```

* Créer un nouveau fichier :

```powershell
    New-Item -Name fichiertest.txt -ItemType file -Value 'Hello World'
    #Ou
    'Hello World' > fichiertest.txt
```


## Supprimer des fichiers/dossiers

* Remove-Item (ri, rm, rd, del)
    * Supprimer tous les fichiers .bak d'un dossier :

    ```powershell
        Remove-Item c:\temp\*.log
    ```

    * Combinaison avec Get-Childitem et récursivité

    ```powershell
        Get-Childitem c:\temp\* - Include *.log -Recurse | Remove-Item
    ```

    * Supprimer les fichiers systèmes/cachés/lecture seule :

    ```powershell
        Remove-Item fichieràsupprimer.txt -Force
    ```
> **Attention !**  
Par défaut, Remove-Item ne demande aucune confirmation. Le paramètre -whatif permet de simuler la commande. Et -confirm demande une confirmation pour chaque suppression de fichier.


### DÉPLACER DES FICHIERS/DOSSIERS

* Move-Item (mi, move, mv)
    * Déplacer tous les fichiers *.Log dans le répertoire logs :
    ```powershell
        Move-Item -Path *.log -destination logs
        Move-Item *.log logs
    ```
    * Déplacer un répertoire et son contenu :
    ```powershell
        Move-Item 'photos vacances' 'mes photos'
    ```
    * Renommer un répertoire avec Move-Item ?


### RENOMMER DES FICHIERS/DOSSIERS

* Rename-Item (ri, ren)

    * Renommer le fichier scriptV1.ps1 par scriptV2.ps1 :
    ```powershell
        Rename-Item -Path scriptV1.ps1 -Newname scriptV2.ps1
        #ou
        Rename-Item scriptV1.ps1 scriptV2.ps1
    ```
    * Renommer le dossier Logs par Logs2010 :
    ```powershell
        Rename-Item -Path Logs -Newname Logs 2010
        #ou
        Rename-Item Logs Logs2010
    ```


### COPIER DES FICHIERS/DOSSIERS :

* Copy-Item (dpi, cp, copy)
    * Copier un fichier vers un autre répertoire :
    ```powershell
        Copy-Item -Path boot.wim -destination d:\RemoteInstall
        #ou
        Copy-Item boot.wim d:\RemoteInstall
    ```
    * Copier une arborescence de répertoires et fichiers :
    ```powershell
        Copy-Item DossierSource DossierDest -Recurse
    ```

> **Copy-Item** crée automatiquement le dossier de destination s'il n'existe pas.



## LES FOURNISSEURS


Précédemment, nous avons fait usage d'un fournisseur sans s'en apercevoir : Filesystem
* Il existe 7 autres fournisseurs :

```powershell
    Get-PSProvider
    
    Name        Capabilities                Drives
    ----        ------------                ------
    WSMan       Credentials                 {WSMan}
    Alias       ShouldProcess               {Alias}
    Environment ShouldProcess               {Env}
    FileSystem  Filter, ShouldProcess       {C, A, D, Z}
    Function    ShouldProcess               {Function}
    Registry    ShouldProcess, Transactions {HKLM, HKCU}
    Variable    ShouldProcess               {Variable}
    Certificate ShouldProcess               {cert}
```


### EXEMPLE AVEC LE FOURNISSEUR ENVIRONMENT

```powershell
    Get-ChildItem ENV:

    Name                      Value
    ----                      ----
    ALLUSERSPROFILE           C:\ProgramData
    APPDATA                   C:\Users\Administrateur\App...
    CommonProgramFiles        C:\Program Files\Common Files
    CommonProgramFiles(x86)   C:\Program Files (x86)\Common...
    CommonProgramW6432        C:\Program Files\Common Files
    ..    SystemRoot          C:\Windows
    TEMP                      C:\Users\ADMINI~1\AppData...
    TMP                       C:\Users\ADMINI~1\AppData...
    USERDOMAIN                VM2K8R2
    USERNAME                  Administrateur
    USERPROFILE               C:\Users\Administrateur
    windir                    C:\Windows
```


* Créer une variable d'environnement :

```powershell
    PS Env:\> New-Item -Name NotreVariable -Value 'PowerShell'
    
    Name    Value
    ----    -----
    Notre   Variable PowerShell
```

* Supprimer une variable d'environnement :

```powershell
    Env:\> Remove-Item NoteVariable
    #ou
    Remove-Item Env:NoteVariable
```

* Récupérer la valeur d'une variable d'environnement :

```powershell
    Get-Content Env:computername
    VM2K8R2
```



## FORMATAGE DE L'AFFICHAGE


### MODES D'AFFICHAGE

Modifier le formatage et les propriétés affichés lors de l'exécution d'une commande.

#### Quatre modes d'affichage :

|Nom          | Alias | Description |
| -------------| ------| --------- |
|Format-Table |ft	   | Affiche les propriétés sous forme de tableau |
|Format-List  |fl	   | Affiche les propriétés sous forme de liste |
|Format-Wide  |fw	   | Affiche une seule propriétés au format large table |
|Format-Custom|fc	   | Affichage personnalisé des propriétés |


### EXEMPLES

* Format-Table avec Get-ChildItem

```powershell
    gci c:\ | Format-Table
    Répertoire : C:\
    Mode  LastWriteTime     Length  Name
    ----  -------------     ------  ----
    d-r-- 29/01/2012 22:45          Program Files
    d-r-- 29/01/2012 21:49          Users
    d---- 30/01/2012 15:37          Windows
```
* Format-List

```powershell
    gci c:\ | Format-List
    Répertoire : C:\
    Name : Users
    CreationTime : 14/07/2009 05:20:08
    LastWriteTime : 29/01/2012 21:49:46
    LastAccessTime : 29/01/2012 21:49:46
    
    Name : Windows
    CreationTime : 14/07/2009 05:20:08
    LastWriteTime : 30/01/2012 15:37:00
    LastAccessTime : 30/01/2012 15:37:00
```


* Choisir les propriétés à afficher :
```powershell
    Get-ChildItem C:\ | Format-List -Property Name
    Répertoire : C:\
    Name : Users
    Name : Windows
```

* Autre exemple avec Get-Process
```powershell
    Get-Process | Format-List -Property id, Name
    Id : 2004
    Name : explorer
    Id : 0
    Name : Idle
    ...
```
* Afficher toutes les propriétés d'un objet :
```powershell
    Get-ChildItem autoexec.bat | Format-List *
```


* Afficher une seule propriété d'un objet :

```powershell
    (Get-ChildItem autoexec.bat).CreationTime
 
    samedi 11 février 2012 21:33:02
```

* Format-List et caractère générique :

```powershell
    Get-ChildItem config.sys | Format-List name, *time
    
    Name : config.sys
    
    CreationTime : 11/02/2012 21:33:02
    LastAccessTime : 11/02/2012 21:33:02
    LastWriteTime : 11/02/2012 21:33:02
```



## SCRIPTING


### QUELQUES RÈGLES

* Utilisation des guillemets doubles ou simples ?

```powershell
$variablea = "Vive"
$variableb = "PowerShell"
Write-Host "$variablea $variableb"
 
Vive PowerShell
 
Write-Host '$variablea $variableb'
 
$variablea $variableb
```
* Les guillemets doubles permettent l'usage de variables (substitution).


* Utilisation des caractères d'échappement (backtick) :

```powershell
Write-Host "$variablec = $variablea $variableb"
= Vive PowerShell
 
Write-Host "`$variablec = $variablea $variableb"
$variablec = Vive PowerShell
 
Write-Host "Ce texte est trop long, `ncouper le en deux."
Ce texte est trop long,
couper le en deux.
```
> **Le backtick en fin de ligne**
indique à PowerShell que la suite se trouve à ligne suivante. Utile pour la lisibilité d'un script.


### LES VARIABLES

* Création et affectation d'une variable :

```powershell
    $nomvariable = 'test'
    #ou 
    Set-Variable -Name 'nomvariable' -Value 'test'
    
    $nomvariable
    test
```

* Obtenir le type d'une variable :

```powershell
    $nomvariable = 'test'
    $nomvariable.GetType()
    
    IsPublic IsSerial Name BaseType
    -------- -------- ---- --------
    True True String System.Object
```

On constate que notre variable est de type 'String' car c'est une chaine caractère.


* Déclarer le type de variable :

```powershell
[int]$var = 15
 
[char]$var =56
$var.GetType()
 
IsPublic IsSerial Name BaseType
-------- -------- ---- --------
True True Char System.ValueType
```

Dans le deuxième exemple, la variable a été forcée en chaine de caractères.

* Convertir une variable de type 'chaine' en type 'int'

```powershell
[int][char]$var = 'B'
$var
 
66
```


* Conversion d'un nombre décimal en hexadecimal :

```powershell
$dec = 1234
$hex = "{0:X}" -f $dec
$hex
4D2
 
$hex.GetType()
 
IsPublic IsSerial Name BaseType
-------- -------- ---- --------
True True String System.Object
```


* Variables prédéfinies (liste non exhautive) :

|Variable | Description |
|---------| ------ |
|$$	      | Contient le dernier mot de la dernière commande tapée dans la console.|
|$?	      | Variable contenant true si la dernière opération a réussi et false dans le cas contraire.|
|$ˆ	      | Contient le premier mot de la dernière commande tapée dans la console.|
|$_	      | Variable contenant l'objet courant transmis par le pipe.|
|$Args	  | Variable contenant un tableau des arguments passés à une fonction ou à un script.|


* Lister toutes les variables :

```powershell
Get-ChildItem variable:
        
Name                    Value
----                    -----
$                       }
?                       True
^                       measure-command
args                    {}
ConfirmPreference       High
ConsoleFileName
DebugPreference         SilentlyContinue
Error                   {Données non valides, Données non valides, Données non valide...
ErrorActionPreference   Continue
ErrorView               NormalView
ExecutionContext        System.Management.Automation.EngineIntrinsics
false                   False
FormatEnumerationLimit  4
HOME                    C:\Users\Baptiste
Host                    System.Management.Automation.Internal.Host.InternalHost
                   ...
```


### TABLEAU À UNE DIMENSION

* Exemple de tableau à une dimension :

|Indice :[0]    | Indice :[1]   |Indice :[2]|
|---------------|---------------|-----------|
|Valeur :16     | Valeur :10    |Valeur :12 |

* Initialiser, puis lire un tableau

```powershell
#Initialisation tableau  #Initialisation avec opérateur de plage (..)
$tab = 16,10,12          $tab = 1..15
$tab[0]                  $tab
16                       1
$tab[0,2]                2
16                       ..
12                       15
```

* Lire le dernier indice d'un tableau :

```powershell
$tab = 1..15
$tab[$tab.Length-1]
15
```


* Concaténer deux tableaux

```powershell
$tableau1 = 'V','I','V','E'
$tableau2 = 'L','I','N','U','X'
$tableau1 + $tableau2
V
I
V
E
L
I
N
U
X
..
```

* Ajouter un élément au tableau

```powershell
$tab = 1,2
$tab += 3
$tab
1
2
3
```


* Modifier la valeur d'un élément :

```powershell
$tab = 'A', 'B'
$tab[0] = 'C'
$tab
C
B
```

* Supprimer un élément d'un tableau :

```powershell
$tab = 12, 13, 20, 30
$tab = $tab[0,1 + 3]
$tab
12
13
30
```


### TABLEAU À DEUX DIMENSIONS
* Possède autant d'index que de dimensions.

* Exemple de tableau à deux dimensions :

|**Indice :[0][0]**|**Indice :[0][1]**|**Indice :[0][2]**|
|--------------|--------------|--------------|
|Valeur :1	   |Valeur :2	  |Valeur :3     |
|**Indice :[1][0]**|**Indice :[1][1]**|**Indice :[1][2]**|
|Valeur :4	   |Valeur :5     |Valeur :6     |
|**Indice :[2][0]**|**Indice :[2][1]**|**Indice :[2][2]**|
|Valeur :7     |Valeur :8     |Valeur :9     |

* Lecture du tableau à deux dimensions :

```powershell
$tab[0]             $tab[2][1]    
1                   8
2
3
```


### TABLEAU ASSOCIATIF (Hashtable)

Un **tableau associatif** n'utilise pas d'indice mais des **clés** utilisées comme identifiants.

* Exemple de tableau associatif :

|Clé            |Valeur |
|---------------|-------|
|Commutateur    |2000   |
|Routeur        |1000   |
|Borne Wifi     |800    |

```powershell
$netItems = @{Commutateur = 2000;Routeur = 1000;'Borne Wifi' = 800}
$netItems
 
Name Value
---- -----                 #Accès via clé : 
Commutateur 2000           $netItems.'Borne Wifi'
Routeur   1000             800
Borne Wifi 800
```


### LES OPÉRATEURS

* Les opérateurs arithmétiques :

|Signe|Signification|
|--|---------------|
|+ |Addition       |
|- |Soustraction   |
|* |Multiplication |
|/ |Division       |
|% |Modulo         |

* Exemples :

```powershell
#Addition de      #Addition et chaines     #Multiplication d'une 
#deux entiers     #de caractères           #chaine de caractères
$int1 = 12        $str1 = 'A'              $str1 = 10 * 'A'              
$int2 = 22        $str2 = 'B'              $str1
$int1 + $int2     $str1 + $str2            AAAAAAAAAA
34                AB
```


* Les opérateurs de comparaison :

|Opérateur|Signification        |
|---------|---------------------|
|-eq      |Egal                 |
|-ne      |Non égal             |
|-gt      |Strictement supérieur|
|-ge      |Supérieur ou égal    |
|-lt      |Strictement inférieur|
|-le      |Inférieur ou égal    |

> **Respect de la casse**  
Les opérateurs ne respectent pas la casse par défaut, pour modifier ce comportement, ajouter "c" avant l'opérateur tel que **-ceq** par exemple.


* Les opérateurs de comparaison générique :

|Opérateur|Signification |
|---------|----------------------------------------------|
|-like    |Comparaison d'égalité d'expression générique  |
|-notlike |Comparaison d'inégalité d'expression générique|

* Exemples d'utilisation :

```powershell
'Powershell' -like '*shell'
True
'Powershell' -like 'power*'
True
'Powershell' -like '*wer*'
True
'Powershell' -like '*wur*'
False
'Powershell' -like '*sh?ll'
True
'power' -like 'po?er'
True
'powwer' -like 'po?er*'
False
```


* Les opérateurs de comparaison des expressions régulières :  

|Opérateur  |Signification  |
|---------  |----------------------------------------------|
|-match     |Comparaison d'égalité entre une expression et une expression régulière|
|-notmatch  |Comparaison d'inégalité entre une expression et une expression régulière|

* Exemples d'utilisation :

```powershell
'Powershell' -match 'power[sun]hell'
True
'Powershell' -match 'powershel[a-k]'
False
'Powershell' -match 'powershel[a-z]'
True
```


* Opérateur de plage
    * Est symbolisé par '..'. Il permet de couvrir une plage de valeurs
    * Exemple d'utilisation :

```powershell
$var1 = 6
$var2 = 10
$var1 .. $var2
6
7
8
9
10
```


* L'opérateur de remplacement permet de remplacer toute ou partie de valeur par une autre.
    * Exemple d'utilisation :
```powershell
'PowerShell' -replace 'Shell', 'Coquillage'
PowerCoquillage
```

Les chaînes de caractères (string) possèdent une méthode appelée **Replace()** qui effectue la même opération :
```powershell
$chaine = 'PowerShell' 'Coquillage'
$chaine.Replace('Shell','Coquillage')
PowerCoquillage
```


* Les opérateurs de type :

|Opérateur  |Signification       |
|---------  |----------------------------------------------|
|-is        |Test si l'objet est du même type.  |
|-isnot     |Test si l'objet n'est pas du même type.|

* Exemples d'utilisation :

```powershell
'Powershell' -is [string]
True
28 -is [int]
True
'A' -is [int]
False
```


* Les opérateurs logiques :

|Opérateur  |Signification           |
|---------  |----------------------------------------------|
|-and	    |Et logique |
|-or	    |Ou logique |
|-not	    |Non logique |
|!	        | Non logique |
|-xor	    |Ou exclusif|

* Exemples d'utilisation :

```powershell
(4 -eq 4) -and (7 -eq 9)
False
(4 -eq 4) -or (7 -eq 9)
True
-not (6 -eq 5)
True
!(6 -eq 5)
True
```


* Les opérateurs d'affectation :

|Notation  classique|Notation raccourcie|
|---------  |---------------------------|
|$i=$i+8    |$i+=8|
|$i=$i-8	|$i-=8|
|$i=$i*8	|$i*=8|
|$i=$i/8	|$i/=8|
|$i=$i%8	|$i%=8|
|$i=$i+1	|$i++|
|$i=$i-1	|$i–|

* Exemple d'utilisation :

```powershell
$i = 0
$i += 21
$i
21
```


* Les opérateurs de redirection :

|Opérateur  |Signification         |
|---------  |---------|
|>          |Redirige le flux vers un fichier, si il existe, il est remplacé.|	
|>>	        |Redirige le flux vers un fichier, si il existe, le flux est ajouté à la fin du fichier.|
|2>&1	    |Redirige les messages d'erreurs vers la standard.|
|2>	        |Redirige les messages d'erreurs vers un fichier, si il existe, il est remplacé.|
|2>>	    |Redirige les messages d'erreurs vers un fichier, si il existe, les messages d'erreurs sont ajoutés à la fin du fichier.|

* Exemples d'utilisation :

```powershell
Get-Process > c:\temp\process.txt
Get-Process >> c:\temp\process.txt
Get-Childitem c:\RepInexistant 2> error.txt
```


* Les opérateurs de fractionnement et de concaténation :

|Opérateur  |Signification         |
|---------  |----------------------------------------------|
|-split	    |Fractionne une chaine en sous-chaine.         |
|-join	    |Concactène plusieurs chaines en une seule.    |

* Exemple de fractionnement :

```powershell
-split "Université de Rouen"
Université
de
Rouen
'Nom:Prenom:Adresse' -split ':'
Nom
Prenom
Adresse
```


* Exemple de concaténation :

```powershell
$tableau ='Janvier', 'Février','Mars'
-join $tableau
JanvierFévrierMars
$tableau -join ', puis '
Janvier, puis Février, puis Mars
```


### PIPELINE

Le pipeline '|' établie un canal de communication entre la sortie d'une commande et l'entrée de la commande qui suit :

```powershell
Get-Command | Out-File c:\fichier.txt
```

> **Pipeline et objets**  
A noter, que contrairement à d'autres langages de script, Powershell ne transfère pas du texte par le pipeline mais des objets.

* Plusieurs pipelines peuvent être utilisé en série :

```powershell
Get-ChildItem C:\Windows | 
ForEach-Object {$_.Get_extension().toLower()} | 
Sort-Object | Get-Unique
```


* La commande Where-Object est couramment utilisé avec le pipeline. Celle-ci filtre les objets passés à travers le pipeline selon les paramètres demandés.

* Exemple - Lister les services démarrés :

```powershell
Get-Service | Where-Object {$_.Status -eq 'Running'}
 
Status  Name    DisplayName
------  ----    -----------
Running ADWS    Services Web Active Directory
Running Appinfo Informations d'application
Running BFE     Moteur de filtrage de base
Running BITS    Service de transfert intelligent en...
....
```


* Exemple - Lister les fichiers de plus de 10 Mo :

```powershell
Get-ChildItem | Where-Object {$_.length -gt 10MB}
 
Répertoire : C:\windows\system32
Mode    LastWriteTime      Length   Name
----    -------------      ------    ----
-a---   29/01/2012 23:33   10886656 ieframe.dll
-a---   14/07/2009 03:28   20268032 imageres.dll
-a---   10/06/2009 22:47   11967524 korwbrkr.lex
-a---   04/01/2012 18:02   54008112 MRT.exe
-a---   29/01/2012 23:33   17786368 mshtml.dll
```


### LES BOUCLES

* Boucle While : Execute un bloc d'instruction en boucle tant que le test conditionnel est vrai :

```powershell
$valeur = 0
while($valeur -ne 3)
    {
    $valeur++
    Write-Host $valeur
    }
```

* Dans cet exemple, tant que la variable est égale à 0,1 ou 2, le bloc d'instruction continue à s'exécuter en boucle.
    * (Valeur condition = **true**)
* Quand la variable prends la valeur 3, une sortie de boucle est provoquée.
    * (Valeur condition = **false**)


* Boucle Do-While : Fonctionne comme While à la différence que le test de condition s'effectue à la fin :

```powershell
Do
{
    Write-Host 'Entrez une valeur de 1 à 5'
    [int]$var = Read-Host
}
While (($var -lt 0) -or ($var -gt 5))
```

* Dans cet exemple, la boucle s'exécutera une fois même si la condition est fausse.
* Le boucle s'arrêtera jusqu'à ce que l'utilisateur saisisse un nombre entre 0 et 5.


* Boucle For : Similaire à While, mais utilise une écriture plus concise.

```powershell
for($valeur=0;$valeur -ne 3;$valeur++)
{
    Write-Host $valeur
}
```

* Dans cette exemple, on peut constater que le résultat est le même qu'avec While mais le code est plus court et plus clair.

> **Assembleur : While VS For**  
Les développeurs en assembleur pourraient y trouver à redire car While serait plus rapide..


* Foreach-Object (alias : Foreach,%) : Commande Powershell parcourant tous les éléments d'une collection.

```powershell
Foreach ($element in Get-Childitem c:\windows)
{
    Write-Host "$($element.Fullname) créé le $($element.creationtime)"
}
 
C:\windows\ADWS créé le 02/12/2012 21:28:04
C:\windows\AppCompat créé le 07/14/2009 05:20:08
C:\windows\AppPatch créé le 07/14/2009 05:20:08
C:\windows\assembly créé le 07/14/2009 05:20:08
C:\windows\Boot créé le 07/14/2009 05:20:09
```


* Foreach-Object et utilisation du pipeline :

```powershell
Get-Process | Foreach{$_.Name} | Sort-Unique
 
conhost
csrss
...
```

* Foreach-Object, begin et process

```powershell
Get-Service | ForEach-Object -Begin {
Write-Host "Début de la liste des services`n"} 
-process {$_.Name} -End {
Write-Host "`nFin de la liste des services"}
 
Début de la liste des services
ADWS
AeLookupSvc
...
Fin de la liste des services
```


### IF, ELSE ET ELSEIF

* La syntaxe d'une structure conditionnelle est la suivante :

```
If (condition)
{
    bloc d'instruction
}
```

* Exemple avec un utilisateur devant entrer la lettre 'A' :

```powershell
$var = Read-Host
If ($var -eq 'A')
{
    Write-Host "Le caractère saisi est 'A'"
}
```


* Un autre exemple avec else :

```powershell
[int]$var1 = Read-Host 'Saisir un nombre'
[int]$var2 = Read-Host 'Saisir un autre nombre'
 
If ($var1 -ge $var2)
{
    Write-Host "$var1 est supérieur ou égal à $var2"
}
Else
{
    Write-Host "$var1 est inférieur à $var2"
}
```


* L'instruction **switch** permet d'éviter une suite de If,else,elseif,elseif...

* Exemple d'utilisation :

```powershell
$Nombre = Read-Host 'Choisir une valeur entre 1 à 5'
 
Switch ($Nombre)
{
    1 {Write-Host 'Le nombre saisi est 1'}
    2 {Write-Host 'Le nombre saisi est 2'}
    3 {Write-Host 'Le nombre saisi est 3'}
    4 {Write-Host 'Le nombre saisi est 4'}
    5 {Write-Host 'Le nombre saisi est 5'}
    Default {Write-Host 'Le nombre saisi est hors plage !'}
}
```


### LES FONCTIONS

* Une fonction correspond à un ensemble d'instructions.
* Permets de gagner du temps en utilisant à nouveau le code déjà créé.
* Participe à la qualité et à la clarté du code.
* Une fonction est constituée des éléments suivants :
  * un nom
  * un type de portée (facultatif)
  * un ou plusieurs arguments (facultatifs)
  * un bloc d'instruction
* Syntaxe d'une fonction :

```
Function [&lt;portée> :] &lt;nom de fonction> (&lt;arguments>)
{
    param (&lt;liste de paramètres>)
    bloc d'instructions
}
```


* Exemple d'utilisation d'une fonction sans arguments :

```powershell
Function Bonjour
{
    $date = Get-Date
    Write-Host "Bonjour, nous sommes le $date"
}
```

* Exemple d'utilisation d'une fonction avec argument :

```powershell
Function Set-Popup
{
    $WshShell = New-Object -ComObject wscript.Shell
    $WshShell.Popup($args[0], 0, 'Popup PowerShell')
}
Set-Popup 'I love Powershell'
```


* Exemple d'utilisation d'une fonction avec paramètres :

```powershell
Function Set-Popup
{
    param([string]$message, [string]$titre)
    $WshShell = New-Object -ComObject wscript.Shell
    $WshShell.Popup($message, 0, $titre)
}
Set-Popup -titre 'Mon Titre' -message 'mon message'
Set-Popup -message 'mon message' -titre 'Mon Titre'
Set-Popup -m 'mon message' -t 'Mon Titre'
```

* Retourner une valeur avec une fonction :

```powershell
Function moyenne
{
    param([double]$nombre1, [double]$nombre2)
    ($nombre1 + $nombre2)/2
}
$resultat = moyenne -nombre1 12 -nombre2 18
$resultat
15
```


### DOTSOURCING

* Le DotSourcing est utilisé pour exécuter le contenu d'un script dans l'étendue courante.
* Ce procédé consiste à placer un point et un espace avant le nom du script.

* Exemple avec la fonction moyenne vue précédemment :

```powershell
./moyenne.ps1
moyenne -nombre1 12 -nombre2 18
Le terme "moyenne" n'est pas reconnu en tant ...
 
. ./moyenne.ps1
moyenne -nombre1 12 -nombre2 18
15
```


### LES FONCTIONS AVANCÉES

* Fonctions équivalentes aux commandlets
* Ajoutent les fonctionnalités suivantes :
  * Paramètres positionnels
  * Paramètres obligatoires
  * Message d'aide sur paramètre
  * et bien plus avec l'attribut cmdletBinding
* Exemple de fonction avancée :

```powershell
Function MoveFile
{
    Param (
    [Parameter(Mandatory=$true,  Position=0, 
    HelpMessage="Chemin du fichier à déplacer")]
    [String]$source,
    [Parameter(Mandatory=$true,  Position=1, 
    HelpMessage="Chemin de destination")]
    [String]$destination)
}
```


* Exemple d'utilisation des paramètres obligatoires et de l'aide :

```powershell
. .\MoveFile #Import de la fonction (Dotsourcing)
MoveFile
applet de commande MoveFile à la position 1 du pipeline de la commande
Fournissez des valeurs pour les paramètres suivants :
(Tapez !? pour obtenir de l’aide.)
source : !?
Chemin du fichier à déplacer
source :
```

>**Explications**  
Les paramètres sont déclarés obligatoires (Mandatory), le shell réclame alors une valeur pour continuer l'exécution.
La combinaison de touche !? permet d'obtenir l'aide déclarée au niveau du paramètre (HelpMessage).



## PERSONNALISATION DU SHELL


### LES PROFILS

* Personnaliser son environnement grâce aux profils.
* Il existe deux types de profils :
  * Les profils utilisateurs - personnalisent l'environnement de l'utilisateur courant.
  * Les profils machines - s'appliquent à tous les utilisateurs de la machine.

* Les profils utilisateurs sont au nombre de deux :

```powershell
%UserProfile%\Mes Documents\WindowsPowerShell\profile.ps1
%UserProfile%\Mes Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
```

* Le premier profil s'applique à tous les environnements utilisateurs, y compris les consoles telle que la console Exchange.
* Le dernier profil s'applique à l'environnement installé par défaut : 'Microsoft.PowerShell'.


* Les profils machines sont aussi au nombre de deux :

```powershell
%Windir%\system32\WindowsPowerShell\v1.0\profile.ps1
%Windir%\system32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1
```

* Pour les machines 64 bits

```powershell
%Windir%\syswow64\WindowsPowerShell\v1.0\profile.ps1
%Windir%\syswow64\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1
```

* Le premier profil s'applique à tous les environnements installés sur la machine pour tous les utilisateurs, y compris les console telle que la console Exchange.
* Le dernier profil s'applique à l'environnement installé par défaut : 'Microsoft.PowerShell'.


* Ordre d'application des profils :

```powershell
%Windir%\system32\WindowsPowerShell\v1.0\profile.ps1
%Windir%\system32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1
%UserProfile%\Mes Documents\WindowsPowerShell\profile.ps1
%UserProfile%\Mes Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
```

* Modifier un profil : la variable $profil contient le chemin du profil utilisateur.

```powershell
$profile
C:\Users\Administrateur\Documents\WindowsPowerShell\
    `Microsoft.PowerShell_profile.ps1
Créer le profil :
New-Item -Path $profile -ItemType file -Force
notepad $profile
```


#### PERSONNALISATION DU FORMATAGE DE L'AFFICHAGE

* Par défaut le retour d'une cmdlet est dirigé vers la commande Out-Default.
* Cette commande gère l'affichage et le formatage des flux d'objets.
* Si le flux d'objets est de type texte, il est redirigé vers Out-Host, dans le cas contraire, Powershell cherchera une vue prédéfinie par rapport au type d'objet retourné.
* Par exemple, les commandes suivantes renvoient le même résultat :

```powershell
Get-ChildItem
Get-ChildItem | Out-Default
Get-ChildItem | Format-Table
Get-ChildItem | Format-Table | Out-Host
Get-ChildItem | Format-Table | Out-String | Out-Host
Get-ChildItem | Format-Table | Out-String | Out-Default
```


* Les vues prédéfinies sont stockées dans des fichiers sous la forme *.format.ps1xml.
* Ces fichiers sont dans le répertoire $PSHOME.
* Il n'est pas conseillé de les modifier directement, car ces fichiers sont signés numériquement.



## GESTION DES FICHIERS


### ÉCRIRE DANS UN FICHIER

* Pour écrire dans un fichier, il existe deux commandes :  
Set-Content et Out-File

```powershell
Get-Process powershell | Set-Content fichier.txt
Get-Content .\fichier.txt
System.Diagnostics.Process (powershell)

Get-Process powershell | Out-File fichier.txt
Get-Content .\fichier.txt
Handles NPM(K) PM(K) WS(K) VM(M) CPU(s) Id   ProcessName
------- ------ ----- ----- ----- ------ --   -----------
526     24     52040 50252 574   0,97   2364 powershell
 
Get-Process powershell | Out-String -stream | Set-Content fichier.txt
 
Get-Content .\fichier.txt
Handles NPM(K) PM(K) WS(K) VM(M) CPU(s) Id   ProcessName
------- ------ ----- ----- ----- ------ --   -----------
526     24     52040 50252 574   0,97   2364 powershell
```


### LIRE DANS UN FICHIER

* Pour lire dans un fichier : commande get-content

```powershell
Get-Process &gt; .\MesProcess.txt
Get-Content MesProcess.txt -TotalCount 5
Handles NPM(K) PM(K) WS(K) VM(M) CPU(s) Id   ProcessName
------- ------ ----- ----- ----- ------ --   -----------
30      4       976  2756  44    0,02   796  conhost
40      6       2116 5212  61    0,34   2624 conhost
439     11      1936 4148  47    0,27   336  csrss
 
C:\scripts\CESI> $file = Get-Content MesProcess.txt
C:\scripts\CESI> $file.Length
46
 
C:\scripts\CESI> 'PowerShell' > file.txt
C:\scripts\CESI> Get-Content .\file.txt -Encoding byte
255 254 80 0 111 0 119 0 101 0 114 0 83 0 104 0 101 0 108 0 108 0 13 0 10 0
``` 


### FICHIER XML

* Un fichier XML est composé de tags pour identifier les informations stockées de manière unique.
  * Exemple de tags : `<Nom>John Smith</Nom>`
  * Exemple avec un attribut : `<univ nom="Université de Rouen" lieu="MSA">...</univ>`
  * Un couple de tags désigne un nœud
  * Exemple complet :

```xml
<?xml version="1.0" ?>
<univ nom="Université de Rouen" lieu="MSA">
    <administratifs>
        <Nom>John Smith</Name>
        <Fonction>Contrôleur Financier</Fonction>
        <Tel>0232000000</Tel>
    </administratifs>
    <administratifs>
        <Nom>James Bond</Name>
        <Fonction>Informaticien</Fonction>
        <Tel>023222000</Tel>
    </administratifs>
</ecole>
```


* Récupérer le fichier xml dans une variable :

```powershell
$xmldata = [xml](Get-Content .\administratifs.xml)
$xmldata.univ.administratifs

Nom         Fonction             Tel
—           ——                   ——
John Smith  Contrôleur Financier 0232000000
James Bond  Informaticien        0232000010
```

* Utilisation du pipeline avec Where-Objet :

```powershell
$xmldata.univ.administratifs | Where-Object {$_.nom -match "James Bond"}
 
Nom         Fonction      Tel
—           ——            ——
James Bond  Informaticien 0232000010
```


* Modifier une donnée :

```powershell
$administratif = $xmldata.univ.administratifs |
    Where-Object {$_.nom -match "James Bond"}
     
$administratif.Fonction = "Responsable Informatique"
$xmldata.univ.administratifs
 
Nom        Fonction                 Tel
—          ——                       ——
John Smith Contrôleur Financier     0232000000
James Bond Responsable Informatique 0232000010
```

* Utilisation de la méthode SelectNodes() :

```powershell
$xmldata.SelectNodes("univ/administratifs")
 
Nom         Fonction                 Tel
—           ——                       ——
John Smith  Contrôleur Financier     0232000000
James Bond  Responsable Informatique 0232000010
```


* Sélection du premier enregistrement :

```powershell
$xmldata.SelectNodes("univ/administratifs[1]")
 
Nom         Fonction             Tel
—           ——                   ——
John Smith  Contrôleur Financier 0232000000
```

* Sélection du dernier enregistrement :

```powershell
$xmldata.SelectNodes("univ/administratifs[last()]")
 
Nom        Fonction                 Tel
—          ——                       ——
James Bond Responsable Informatique 0232000010
```


* Lister le ou les attributs d'un tag :

```powershell
$xmldata.ecole.Get_Attributes()
 
#Text
—–
ENSAN
Rouen
```

* Lire un attribut :

```powershell
$xmldata.ecole.GetAttribute("lieu")
 
Rouen
```

* Créer ou modifier un attribut :

```powershell
$xmldata.ecole.SetAttribute("lieu","Darnétal")
$xmldata.ecole.GetAttribute("lieu")
 
Darnétal
```


* Ajouter un nouveau noeud :

```powershell
#CreerNodeXml.ps1
#Chargement du fichier XML
$xmldata = [xml](Get-Content administratifs.xml)
 
#Création d'un nœud
$newadministratif = $xmldata.CreateElement("administratif")
$newadministratif.set_InnerXML('
    "<nom>Paul Atréides</nom><fonction>Consultant</fonction>"')
 
# Ecriture du nœud
$xmldata.univ.AppendChild($newadministratif)
 
# Vérification du résultat
$xmldata.univ.administratifs
 
# Affichage flux xml
$xmldata.get_InnerXml()
```



## SÉCURITÉ


### SÉCURITÉ ET SCRIPTS

* PowerShell propose une meilleur sécurité par défaut :
* Les fichiers de scripts 'ps1' sont associés au bloc-note.
* Par défaut, l'exécution de scripts est désactivée.  
* PowerShell propose quatre stratégies d'exécution de scripts :
  * Restricted : Aucun scripts ne peut s'exécuter .
  * Allsigned : Tous les scripts doivent signés numériquement.
  * RemotedSigned : Les scripts locaux peuvent être exécuté, les scripts externes doivent être signés.
  * Unrestricted : Tous les scripts peuvent être exécutés.

```powershell
.\Get-ConsoleAsText.ps1
Impossible de charger le fichier C:\Get-ConsoleAsText.ps1, 
car l'exécution de scripts est désactivée sur ce système.
...
```


* Identifier la stratégie d'exécution courante :

```powershell
Get-ExecutionPolicy
 
Restricted
```

* Appliquer une stratégie d'exécution :

```powershell
Set-ExecutionPolicy RemoteSigned
```


### SIGNATURE NUMÉRIQUE D'UN SCRIPT

* La signature numérique d'un script permet de garantir qu'il n'a pas été modifié.
* La signature est générée à partir d'une clé privé.
* L'authenticité du script est vérifié à l'aide d'une clé publique.
* Il est possible d'acheter un certificat auprès d'une autorité de certification reconnue.



## WMI & CIM


### PRÉSENTATION DE WMI

* WMI (Windows Management Instrumentation) est née à l'initiative du groupe DMTF (Distributed Management Task Force)
* La norme CIM (Common Information Model) est issue de ce groupe.
* CIM est un schéma orienté objet permettant la gestion système, réseaux, applications, BDD et périphériques.
* Néanmoins c'est Windows qui intégre le plus cette norme avec WMI.
* Pour plus d'informations sur WMI :

http://laurent-dardenne.developpez.com/articles/wmi-p1/
http://dotnet.developpez.com/articles/wmi1/100/1


### EXEMPLES

* Exemple d'une commande WMI avec Powershell

```powershell
get-wmiobject win32_operatingsystem | select InstallDate, Caption
 
InstallDate               Caption
-----------               -------
20120129214801.000000+060 Microsoft Windows Server 2008 R2 Standard
```

> **Espace de nom par défaut**
A noter, que par défaut, la commande Get-WmiObject porte sur l'espace de nom root\cimv2


* Autres exemples :

```powershell
get-wmiobject win32_bios -computername W2K8R2
 
SMBIOSBIOSVersion : 6.00
Manufacturer : Phoenix Technologies LTD
Name : PhoenixBIOS 4.0 Release 6.0
SerialNumber : VMware-56 4d da 0d 44 23 ac cd-dd ca d2 Version : INTEL - 6040000
 
get-wmiobject win32_ntdomain
 
ClientSiteName : Default-First-Site-Name
DcSiteName : Default-First-Site-Name
Description : DOM
DnsForestName : dom.local
DomainControllerAddress : \\192.168.97.160
DomainControllerName : \\VM2K8R2
DomainName : DOM
Status : OK
```