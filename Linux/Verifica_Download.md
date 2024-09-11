
Esempio su ubuntu 24.04 live-server usato per nodo Bitcoin

1 mi posiziono su cartella Donwload o cartella dedicata comando cd

2 scarico il file, solito comando wget attenzione trgz è un file compresso va decompresso dopo

3 SHA256SUM  è un file di testo che raccohlie hash di tutti i file un  Hash per ogni file perchè sappiamo che è univoco

![alt text](../Images/SHA256SUMS.JPG)

4 SHA256.gpg o arc è la firma del file SHA256SUMS

5 usabdo il comando gpg --verify SHA256SUMS.gpg SHA256SUMS verifico la firma e ottengo la chiave pubblica del firmatario