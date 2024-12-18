# MBED sur windows

## Installation des outils Mbed sur Windows

Liens à consulter : 
- Ce qui suit est une quasiment copie du contenu de ce lien :
https://github.com/eirbot/mbed-os-template-eirbot/blob/main/README.md
- Autre lien utile :
https://www2.ciel-kastler.fr/docs/mbed6tron/


### Installation du compilateur ``ARM GCC``

Quelle que soit la manière d'installer les outils Mbed sur votre machine, il vous faut d'abord installer la chaine de compilation nécessaire pour compiler un projet Mbed. La dernière version officielle (maj du 1er mars 2023) est la 10.3-2021.07, recommandée depuis MbedOs 6.16.

- Télécharger et lancer l'installation de GCC GNU ARM 10.3-2021.07 :
https://developer.arm.com/-/media/Files/downloads/gnu-rm/10.3-2021.07/gcc-arm-none-eabi-10.3-2021.07win32/gcc-arm-none-eabi-10.3-2021.07-win32.exe


- ATTENTION : à la fin de l'installation, bien cocher "Add path to environment variable".

- Optionnel : Pour vérifier l'installation, ouvrir une invite de commande (clique droit > "Cmder here") et taper `arm-none-eabi-gcc --version`

```shell
PS C:\Users\felix\Documents\mbed\demo-install-mbed> arm-none-eabi-gcc --version
arm-none-eabi-gcc.exe (Arm GNU Toolchain 13.3.Rel1 (Build arm-13.24)) 13.3.1 20240614
Copyright (C) 2023 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

### Autres installations : Git, Mercurial/TortoiseHG

Pour installer ``Git for Windows`` : 
https://gitforwindows.org/

Pour Télécharger et installer ``Mercurial/TortoiseHG`` (nécessaire pour Mbed CLI) : 
https://www.mercurial-scm.org/release/tortoisehg/windows/tortoisehg-6.3.2-x64.msi

### Installation de Python 3.7.9, version actuellement supportée par MbedCLI 1:

Si vous avez Python 2.7 d'installée, vous devez quand même installer la 3.7.

Si vous avez une version trop récente de python (genre 3.11), vous devez quand même installer la 3.7, ce n'est pas un problème, plusieurs versions de Python peuvent coexister sur un même OS, il faut juste ne pas se tromper sur celle qu'on appelle ...

Note : Il est possible d'installer Mbed CLI sous Python 3.11, mais au prix d'un long processus d'installation des outils Visual Studio Build Tool. Sauf si vraiment vous voulez le faire, je vous conseille plutôt d'installer la 3.7 .

Télécharger et lancer l'installation Python 3.7.9 : https://www.python.org/ftp/python/3.7.9/python-3.7.9-amd64.exe

ATTENTION : Bien s'assurer de cocher "Add python.exe to PATH", puis faire "Install Now"
À la fin de l'installation, faites le "Disable Path length limit" (https://www.youtube.com/watch?v=3UQrKchr9s0&t=254s).

### Vérification des outils git, mercurial, python et compilateur 

Vérifier que les commandes `git`, `hg`, `python` et `arm-none-eabi-gcc` fonctionnent :

```shell
PS C:\Users\felix\Documents\mbed\demo-install-mbed> git --version 
git version 2.47.0.windows.2
PS C:\Users\felix\Documents\mbed\demo-install-mbed> hg --version 
Mercurial Distributed SCM (version 6.5.1)
PS C:\Users\felix\Documents\mbed\demo-install-mbed> python --version
Python 3.7.9
PS C:\Users\felix\Documents\mbed\demo-install-mbed> arm-none-eabi-gcc --version
arm-none-eabi-gcc.exe (Arm GNU Toolchain 13.3.Rel1 (Build arm-13.24)) 13.3.1 20240614
Copyright (C) 2023 Free Software Foundation, Inc.
```

### Installer Mbed-CLI 1.10.5

Mettre à jour ``pip`` : 

```shell
python.exe -m pip install --upgrade pip
```

Installer ``pipx`` pour gérer des environnements isolés (ne pas tenir compte des warnings sur le path) : 
```shell
pip install --user pipx 
```

Mettre à jour ses variables d'environnements Windows : 
```shell
python.exe -m pipx ensurepath
```

Redémarrer son terminal (fermer et rouvrir).

Installer Mbed-CLI 1.10.5 à l'aide de pipx : 

```shell
$ pipx install mbed-cli
  installed package mbed-cli 1.10.5, installed using Python 3.7.9
  These apps are now globally available
    - mbed-cli.exe
    - mbed.exe
done! ✨ 🌟 ✨
```

Vérifier son installation : 

```shell 
$ mbed --version
1.10.5```
```

### Installer sixtron_flash

``sixtron_flash`` est l’utilitaire fourni par 6tron pour flasher le microcode des cartes Zest Core. 

Pour l'installer :

```shell
pipx install git+https://github.com/catie-aq/6tron_flash.git#egg=sixtron_flash
```
 Pour l'exécuter :

 ```shell
 sixtron_flash
 ```

## Votre premier projet ``mbed`` 

(Avec une session `bash`)

Importer le projet ``blinky`` : mbed import https://github.com/...

```shell 
felix@FELIX6604 CLANGARM64 ~/Documents/mbed (master)
$ ls -l
drwxr-xr-x 1 felix 197121 0 nov.  15 15:57  mbed-os-example-blinky/
cd mbed-os-example-blinky
```

```shell
$ mbed deploy
[mbed] Working path "C:\Users\felix\Documents\mbed\mbed-os-example-blinky\mbed-os-example-blinky" (library)
[mbed] Program path "C:\Users\felix\Documents\mbed\mbed-os-example-blinky\mbed-os-example-blinky"
[mbed] Updating library "mbed-os" to rev #17dc3dc2e6e2 (tags: mbed-os-6.17.0, mbed-os-6.17.0-rc1)
```

```shell
felix@FELIX6604 CLANGARM64 ~/Documents/mbed/mbed-os-example-blinky/mbed-os-example-blinky (master)
$ mbed compile
[mbed] Working path "C:\Users\felix\Documents\mbed\mbed-os-example-blinky\mbed-os-example-blinky" (library)
[mbed] Program path "C:\Users\felix\Documents\mbed\mbed-os-example-blinky\mbed-os-example-blinky"
[Warning] @,: Compiler version mismatch: Have 13.3.1; expected version >= 9.0.0 and < 10.0.0
Building project mbed-os-example-blinky (ZEST_CORE_STM32L4A6RG, GCC_ARM)
Scan: mbed-os-example-blinky
Link: mbed-os-example-blinky
Elf2Bin: mbed-os-example-blinky
| Module                           |     .text |    .data |     .bss |
|----------------------------------|-----------|----------|----------|
| [fill]                           |    70(+0) |    0(+0) |   36(+0) |
| [lib]\c.a                        |  5100(+0) | 1376(+0) |  373(+0) |
| [lib]\gcc.a                      |   752(+0) |    0(+0) |    0(+0) |
| [lib]\misc                       |   264(+0) |    4(+0) |   25(+0) |
| main.o                           |    48(+0) |    0(+0) |    0(+0) |
| mbed-os\cmsis                    |  7002(+0) |  168(+0) | 6208(+0) |
| mbed-os\drivers                  |   150(+0) |    0(+0) |    0(+0) |
| mbed-os\hal                      |  1556(+0) |    8(+0) |  114(+0) |
| mbed-os\platform                 |  5616(+0) |  260(+0) |  424(+0) |
| mbed-os\rtos                     |    32(+0) |    0(+0) |    0(+0) |
| mbed-os\targets                  | 10756(+0) |    8(+0) | 1052(+0) |
| zest-core-stm32l4a6rg\TARGET_STM |   714(+0) |    0(+0) |    0(+0) |
| Subtotals                        | 32060(+0) | 1824(+0) | 8232(+0) |
Total Static RAM memory (data + bss): 10056(+0) bytes
Total Flash memory (text + data): 33884(+0) bytes

Image: .\BUILD\ZEST_CORE_STM32L4A6RG\GCC_ARM\mbed-os-example-blinky.bin
```

```shell
$ sixtron_flash
6TRON Flash Tool
  No argument provided: finding binary automatically...
  Found binary at BUILD/ZEST_CORE_STM32L4A6RG/GCC_ARM/mbed-os-example-blinky.bin
Flash: BUILD/ZEST_CORE_STM32L4A6RG/GCC_ARM/mbed-os-example-blinky.bin
SEGGER J-Link Commander V8.10g (Compiled Nov 14 2024 09:06:35)
DLL version V8.10g, compiled Nov 14 2024 08:59:00

J-Link Commander will now exit on Error

J-Link Command File read successfully.
Processing script file...
J-Link>r
J-Link connection not established yet but required for command.
Connecting to J-Link via USB...FAILED: Cannot connect to J-Link.

Script processing completed.

Error when running J-Link executable. Please verify that a J-Link probe is connected, and that JLink.exe has been added to the PATH
```

## Votre deuxième projet ``mbed``

Aller dans vos documents, puis ouvrir un terminal, et importer le code de la ``station`` de NAMeC : 

```shell
git clone -b 3antennas-all-bots https://github.com/NAMeC-team/base_station base_station
```

Toutes les commandes ``mbed`` sont à faire à la racine du projet. 

```shell
cd base_station
```

Pour déployer le projet (``MbedCLI`` installe tous les paquets Python manquants...)

```shell
mbed deploy
```

Constater que :
- le dossier "mbed-os" a été ajouté, 
- et plein d'autres modifications dans le répertore de votre projet...

Préciser la cible pour la compilation :

```shell
cp zest-core-stm32l4a6rg/custom_targets.json . 
```



Pour compiler le projet : 
```shell
mbed compile
```

## Déboguer avec `J-Link EDU Mini` (via VSCode)

1. **J-Link EDU Mini**

La J-Link EDU Mini est une sonde de débogage économique de SEGGER, conçue pour des usages éducatifs. Elle supporte les microcontrôleurs ARM Cortex-M et offre les fonctionnalités suivantes :

- **Débogage** : Permet le débogage des applications embarquées.
- **Programmation** : Supporte la programmation des microcontrôleurs.
- **Compatibilité** : Compatible avec les environnements de développement populaires comme vscode.

2. **Extension Cortex-Debug**

Installer l'extension `Cortex-Debug` qui prend en charge le débogage des microcontrôleurs ARM Cortex-M avec la sonde  `J-Link EDU Mini` (voir documentation).

3. **Configurer votre espace de travail : le fichier `launch.json`**

Dans le dossier `.vscode` (à créer s'il n'existe pas), ajoutez le fichier `launch.json` avec la configuration suivante :

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug ROBOT with JLink",
            "cwd": "${workspaceFolder}",
            "executable": "./robot/BUILD/ZEST_CORE_STM32L4A6RG/GCC_ARM/robot.elf",
            "request": "launch",
            "type": "cortex-debug",
            "device": "STM32L4A6RG",
            "runToEntryPoint": "main",
            "showDevDebugOutput": "none",
            "interface": "swd",
            "servertype": "jlink"
        }
    ]
}
```
La ligne :
```json
            "executable": "./robot/BUILD/ZEST_CORE_STM32L4A6RG/GCC_ARM/robot.elf",
```
est à adapter pour cibler votre fichier binaire (`.elf`).


4. **Lancer le débogage** :
    - Connectez la J-Link EDU Mini à votre microcontrôleur et à votre ordinateur.
    - Cliquez sur `Start Debug Session` pour lancer le débogage avec la configuration souhaitée.

Le debuger chargera votre programme en mémoire (s'il n'est pas déjà flashé) et démarrera le débogage.

Vous êtes maintenant en mesure de déboguer vos applications embarquées en utilisant la J-Link EDU Mini directement depuis VSCode.

Fonctionnalités :

- Breakpoints : Ajoutez des points d'arrêt dans ton code pour suspendre l'exécution.
- Step In/Out/Over : Exécutez le code pas à pas pour observer le comportement.
- Inspecter les variables : vous pouvez voir la valeur des variables globales, locales ou même des registres.
- Arrêter et analyser l'exécution

À tout moment, vous pouvez Suspendre ou Stopper l'exécution pour inspecter l'état du microcontrôleur.

- Résumé des commandes/raccourcis utiles :
    - F5	Démarre/continue le débogage
    - F10	Exécute la ligne courante (Step Over/Pas à pas principal)
    - F11	Entre dans la fonction (Step In/Pas à pas détaillé)
    - Shift + F11	Sort de la fonction (Step Out/Pas à pas sortant)
    - Shift + F5	Arrêter le débogage

