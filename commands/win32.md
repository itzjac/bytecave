# WIN+R
* dxdiag
* service.msc
* regedit
* iexplorer

## ".emacs" 
* rn .emacs.txt .emacs


## Strip out pdbs
* del /s /q *.pdb
* rmdir /s /q *.pdb


## Strip out source & Intermediate directories (should be %% if in a bat)
* FOR /d /r . %d IN (Source) DO @IF EXIST "%d" rd /s /q "%d"
* FOR /d /r . %d IN (Intermediate) DO @IF EXIST "%d" rd /s /q "%d"


## Recursively search directories
* dir /s [DirName|Filename]

## Recursively find a string in directory tree
* findstr /spin /c:"version" *.h
