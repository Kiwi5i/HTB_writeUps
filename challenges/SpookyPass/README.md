# Spooky Pass

Esse desafio foi o mais simples possível de engenharia reversa

Eu tinha um arquivo ELF, ao executa-lo ele pedia uma senha, se eu a errasse o programa encerrava sem me dar nada.

![formato do programa](IMG1.png)

Primeiramente eu abri o programa no ghidra e fui direto para a main. Depois de pedir a senha, o programa a comparava com a string correta em plaintext.

![decompile](IMG2.png)

Então foi só usá-la como senha e conseguir a flag: HTB{un0bfu5c4t3d_5tr1ng5}

![flag](IMG3.png)
