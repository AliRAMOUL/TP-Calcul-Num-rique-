# TP-Calcul-Num-rique- 



# **Rapport 1 - TD/TP 2 et 3 - Algèbre linéaire dense**

## Introduction

Les travaux suivant ont été réalisé durant les scéances de TP 2 & 3. Ces scéances ont portés sur la découverte de l'outil `Scilab`, et de l'implémentation de divers algorithme. Le but principal de ce TP est de nous familiariser avec `Scilab`, ainsi que d'explorer différentes version d'un même algorithme, comparer les performances et l'erreur numérique entre nos implémentations, et celles présen:e de base dans `Scilab`.

[Dépot distant du TP](https://github.com/M5ssss/9foexXTWeg) (contient le fichier .md ainsi que les fichiers source de certaines fonctions demandées)


# Compte Rendu TP2

## Exercice 6

### 1.
    --> x = [1,2,3,4]
    x  = 

    1.   2.   3.   4.

### 2.
    --> y = [1;2;3;4]

    y  = 

    1.
    2.
    3.
    4.

### 3.
#### a)
    --> z = x + y'
    z  = 

    1.   4.   6.   8.
#### b)
    s = x*y
    s  = 

    30.

### 4.
#### a)
    --> size(x)
    ans  =

    1.   4.
#### b)
    --> size(y)
    ans  =

    4.   1.

### 5.
    --> norm(x)
    ans  =

    5.4772256

    --> norm(x,2)
    ans  =

    5.4772256

### 6.
    --> A = [1,2,3;4,5,6;7,8,9;10,11,12]
    A  = 

    1.    2.    3. 
    4.    5.    6. 
    7.    8.    9. 
    10.    11.   12.

### 7.
    --> A'
    ans  =

    1.   4.   7.   10.
    2.   5.   8.   11.
    3.   6.   9.   12.

### 8.
    -->A = [1,2,3;4,5,6;7,8,9]
    A  = 

    1.   2.   3.
    4.   5.   6.
    7.   8.   9.

    -->B = [9,8,7;6,5,4;3,2,1]
    B  = 

    9.   8.   7.
    6.   5.   4.
    3.   2.   1.

    --> A + B
    ans  =

    10.    10.   10.
    10.    10.   10.
    10.    10.   10.

    --> A - B
    ans  =

    -8.  -6.  -4.
    -2.   0.   2.
    4.   6.   8.

    --> A * B
    ans  =

    30.     24.    18.
    84.     69.    54.
    138.     114.   90.

### 9.
    --> cond(A)
    ans  =

    3.813D+16

## Exercice 7
### 1.
    --> A = rand(3,3)
    A  = 

    0.2113249   0.3303271   0.8497452
    0.7560439   0.6653811   0.685731 
    0.0002211   0.6283918   0.8782165

### 2.
    --> xex = rand(3,1)
    xex  = 

    0.068374 
    0.5608486
    0.6623569

### 3.
    --> b = A * xex
    b  = 

    0.7625473
    0.8790705
    0.9341406

### 4.
    --> A\b
    ans  =

    0.068374 
    0.5608486
    0.6623569

### 5.
Pour pouvoir visualiser l'erreur avant et l'erreur arrière, il faut modifier la précision maximale des résultats de scilab. La précision par défault est de 10 chiffres significatifs. La précision maximale est de 25 chiffres significatifs. Pour la changer il faut entrer la commande suivante: `format('v', 25)`

Cela nous donne:
    
    A  = 

    0.211324865464121103287    0.3303270917385816574097   0.8497452358715236186981
    0.7560438541695475578308   0.6653811042197048664093   0.685731019824743270874 
    0.000221134629100561142    0.6283917883411049842834   0.8782164813019335269928

    ───────────────────────────

    xex  = 

    0.0683740368112921714783
    0.5608486062847077846527
    0.6623569373041391372681

    ───────────────────────────

    b  = 

    0.7625472750706951963195
    0.8790705333713020319664
    0.9341405574043006865281
    
    ───────────────────────────

    A\b = 

    0.0683740368112918106558
    0.5608486062847081177196
    0.6623569373041391372681

**Erreur avant:**

    --> erreur_avant = norm(xex - A\b)/norm(xex)
    erreur_avant  =

    0.0000000000000005640326

**Erreur arrière:**

    erreur_arriere = norm(b-A*(A\b)))/(norm(A)*norm(A\b))
    erreur_arriere  = 

    0.0000000000000001604324

Selon la règle des erreurs avant et arrière, l'erreur avant est inférieure ou égale au conditionnement de A par l'erreur arrière.

Dans notre cas:

    erreur_avant <= cond(A) * erreur_arriere
    ans  =

    T

Donc les résultats obtenus sont en adéquation avec les résultats attendus.

### 6.
**n = 100:**

    erreur_avant =      0.0000000000000362265609
    erreur_arriere =    0.0000000000000002937998

**n = 1000:**

    erreur_avant =      0.0000000000004651308118
    erreur_arriere =    0.0000000000000015613118

**n = 10000:**

    erreur_avant =      0.0000000008160238809582
    erreur_arriere =    0.0000000000000074851387

Nous pouvons remarquer que la valeur de l'erreur avant et arriere augmente, car chaque valeur dans le tableau est soumise à une erreur 'naturelle' dû au stockage fini des valeurs floattante en mémoire, ces erreures s'additionne, et nous constantons une augmentation de l'erreur avec l'augmentation de la taille de la matrice. 

## Exercice 8

### 1.
**matmat3b.sci**

```Scilab
    function [C] = matmat3b(A,B)

        [m,p] = size(A)
        [p,n] = size(B)
        C = zeros(m,n)
        for i = 1 : m
            for j = 1 : n
                for k = 1 : p
                    C(i,j) = A(i,k) * B(k,j) + C(i,j)
                end
            end
        end

    endfunction
```
### 2.

**matmat2b.sci**

```Scilab
    function [C] = matmat2b(A,B)

        [m,p] = size(A)
        [p,n] = size(B)
        C = zeros(m,n)
        for i = 1 : m
            for j = 1 : n
                C(i,j) = A(i,:) * B(:,j) + C(i,j);
            end
        end

    endfunction
```
**matmat1b.sci**

```Scilab
    function [C] = matmat3b(A,B)

        [m,p] = size(A)
        [p,n] = size(B)
        C = zeros(m,n)
        for i = 1 : m
            C(i,:) = A(i,:) * B + C(i,:);
        end

    endfunction
```
### 3.

Les performances sont mesurées avec des tailles de n = {10x10, 100x100, 1000x1000}.

commande: `tic(); matmatXb(A,B); toc()`

**n = 10x10:**

    matmat3b: 0.0025650 sec
    matmat2b: 0.0008170 sec
    matmat1b: 0.0001720 sec
**n = 100x100:**

    matmat3b: 1.156247 sec
    matmat2b: 0.035175 sec
    matmat1b: 0.005717 sec
**n = 1000x1000:**

    matmat3b: 1161.2225 sec
    matmat2b: 11.334808 sec
    matmat1b: 2.5810250 sec

### 4.

Nous pouvons constater que l'algorithme 1b est plus rapide que l'algorithme 2b, lui même plus rapide que l'algorithme 3b.

La difference de temps d'execution entre les différents algorithmes augmente de façon exponentielle en fonction de la taille de la matrice, passant d'un rapport de 15 à 450 entre la fonction 1b et 3b.

# Compte Rendu TP3

## Exercice 2

### 1.

`usolve.sci`

```Scilab
    function [x] = usolve(U,b)
    
        [n,n] = size(U)
        x = zeros(n)
        x(n) = b(n) / U(n,n)
        for i = n-1:-1:1
            x(i) = (b(i) - U(i,(i+1):n) * x((i+1):n)) / U(i,i)
        end

    endfunction
```
`lsolve.sci`

``` Scilab
    function [x] = lsolve(L,b)

        [n,n] = size(L)
        x = zeros(n)
        x(1) = b(1) / L(1,1)
        for i = 2 : n
            x(i) = (b(i) - L(i, 1:(i-1)) * x(1:(i-1))) / L(i, i)
        end

    endfunction
```

### 2.
**Import et initialisation de A & b**
    
    --> exec('lsolve.sci',-1)
    --> exec('usolve.sci',-1)
    --> A = rand(5,5)
    A  = 

    0.9222899   0.2615761   0.1199926   0.672395    0.4829179
    0.9488184   0.4993494   0.2256303   0.2017173   0.2232865
    0.3435337   0.2638578   0.6274093   0.3911574   0.8400886
    0.3760119   0.5253563   0.7608433   0.8300317   0.1205996
    0.7340941   0.537623    0.0485566   0.587872    0.2855364

    --> b = rand(5,1)
    b  = 

    0.8607515
    0.8494102
    0.5257061
    0.993121 
    0.6488563

> **Evaluation de usolve()**
>
>       --> usolve(triu(A),b) == triu(A)\b
>       ans  =
>
>       F
>       T
>       T
>       T
>       T
>
> La solution de la fonction usolve() n'est pas égale à la solution donnée par l'opérateur `\`. Cependant, si l'on affiche les valeurs:
>
>       --> triu(A)\b
>       ans  =
>
>       -0.9778049
>        1.5752441
>       -2.7449172
>        0.8663152
>        2.2724117
>
>       --> usolve(triu(A), b)
>       ans  =
>
>       -0.9778049
>        1.5752441
>       -2.7449172
>        0.8663152
>        2.2724117
> 
> On constate qu'elles sont similaires pour une précision de 10. La différence viens donc d'un chiffre significatif très petit. L'algorithme renvoit des valeurs similaires mais avec une précision différente. Cela est sans doute dû au fait que l'opérateur `\` est implémenté plus "profondement" que notre fonction, et bénéficie donc d'optimisation et de correction.
> L'algorithme est donc correcte mais les valeurs ne sont pas précise.

> **Evaluation de lsolve()**
>
>       --> lsolve(tril(A),b) == tril(A)\b
>       ans  =
>
>       F
>       F
>       T
>       F
>       T
> La solution de la fonction lsolve() n'est pas égale à la solution donnée par l'opérateur `\`. Cependant, si l'on affiche les valeurs:
> 
>       --> tril(A)\b
>       ans  =
>
>       0.9332765
>       -0.0722936
>       0.3572937
>       0.4919492
>       -1.0644592
>
>       --> lsolve(tril(A),b)
>       ans  =
>
>       0.9332765
>       -0.0722936
>       0.3572937
>       0.4919492
>       -1.0644592
> 
> On constate qu'elles sont similaires pour une précision de 10. La différence viens donc d'un chiffre significatif très petit. L'algorithme renvoit des valeurs similaires mais avec une précision différente. Cela est sans doute dû au fait que l'opérateur `\` est implémenté plus "profondement" que notre fonction, et bénéficie donc d'optimisation et de correction.
> L'algorithme est donc correcte mais les valeurs ne sont pas précise.

## Exercice 3

### 1.

`gausskij3b.sci`
``` Scilab
    function [x] = gausskij3b(A,b)

        [n,n] = size(A)
        for k = 1 : n - 1
            for i = k + 1 : n
                Mik = A(i,k) / A(k,k)
                b(i) = b(i) - Mik * b(k)
                for j = k + 1 : n
                    A(i,j) = A(i,j) - Mik * A(k,j)
                end
            end
        end

        x = usolve(A,b)
    
    endfunction
```

### 2.

**(n = 5)**
    --> exec('usolve.sci',-1)
    --> exec('gausskij3b.sci',-1)

    --> A = rand(5,5)
    A  = 

    0.4368588   0.0437334   0.1280058   0.1531217   0.8784126
    0.2693125   0.4818509   0.7783129   0.6970851   0.113836 
    0.6325745   0.2639556   0.211903    0.8415518   0.1998338
    0.4051954   0.4148104   0.1121355   0.4062025   0.5618661
    0.9184708   0.2806498   0.6856896   0.4094825   0.5896177

    --> b = rand(5,1)
    b  = 

    0.6853980
    0.8906225
    0.5042213
    0.3493615
    0.3873779

    --> gausskij3b(A,b)
    ans  =

    -1.1494717
    -0.9651368
     0.8107313
     1.3116728
     1.0531949

    --> A\b
    ans  =

    -1.1494717
    -0.9651368
     0.8107313
     1.3116728
     1.0531949

Les valeurs sont encore une fois visuellement similaires, mais si l'on effectue `gausskij3b(A,b) == A\b`, le résultat est faux, indiquant que l'algorithme de gauss implementé n'est qu'une approximation du résultat réel.

Des tailles superieures ont été testée (10, 25 & 50). Dans les 3 cas, l'algorithme de gauss fourni une réponse avec un temps d'execution correcte, alors que l'utilisation de l'operation `A\b` prend beaucoup plus de temps et fini irremediablement par faire crasher le logiciel scilab.

On peut en conclure que l'algorithme de `gausskij3b()` est une alternative correcte à l'operateur `\` si l'on est peu regardant concernant la précision.

## Exercice 4

### 1.
`mylu3b.sci`

```Scilab
function [L,U] = mylu3b(A)

    [n,n] = size(A)

    for k = 1 : n - 1
        for i = k + 1 : n
            A(i,k) = A(i,k) / A(k,k)
        end
        for i = k + 1 : n
            for j = k + 1 : n
                A(i,j) = A(i,j) - A(i,k) * A(k,j)
            end
        end
    end

    L = tril(A,-1)
    U = triu(A)

    for i = 1 : n
        L(i,i) = 1
    end

endfunction    
```

### 2.

**(n = 5)**

    --> A = rand(5,5);[a,b] = lu(A)
    a  = 

    1.          0.          0.          0.          0.
    0.3415034   1.          0.          0.          0.
    0.3619963   0.4564216   1.          0.          0.
    0.8435645   0.4107318  -0.6976776   1.          0.
    0.8507078  -0.1419772   0.3659657   0.3145011   1.
    
    b  = 

    0.8641141   0.262044   0.8618523   0.840882    0.3123632
    0.          0.694823   0.3760868   0.5379032   0.0435962
    0.          0.         0.4817267  -0.4738505  -0.020919 
    0.          0.         0.         -0.4182567   0.0135524
    0.          0.         0.          0.          0.2786679

    --> [c,d] = mylu3b(A)
    c  = 

    1.          0.          0.          0.          0.
    0.3415034   1.          0.          0.          0.
    0.3619963   0.4564216   1.          0.          0.
    0.8435645   0.4107318  -0.6976776   1.          0.
    0.8507078  -0.1419772   0.3659657   0.3145011   1.
    d  = 

    0.8641141   0.262044   0.8618523   0.840882    0.3123632
    0.          0.694823   0.3760868   0.5379032   0.0435962
    0.          0.         0.4817267  -0.4738505  -0.020919 
    0.          0.         0.         -0.4182567   0.0135524
    0.          0.         0.          0.          0.2786679

>

    --> A - a * b
    ans  =

    0.          0.          0.   0.          0.
    0.          0.          0.   0.          0.
    0.          5.551D-17   0.   1.110D-16   0.
    0.          0.          0.  -2.220D-16   0.
    1.110D-16  -1.388D-17   0.   0.          0.

    --> A - c * d
    ans  =

    0.   0.   0.          0.          0.
    0.   0.   0.          0.          0.
    0.   0.  -1.110D-16   0.          0.
    0.   0.   0.         -1.110D-16   0.
    0.   0.   0.          5.551D-17   0.

On peut remarquer que les deux résultats sont encore une fois différents. Cependant, les résultats obtenus avec l'algorithme `mylu3b()` semblent plus précis que les résultats de la fonction `lu()` par défaut. En effet, A - LU doit retourner une matrice de 0. Hors ici, la matrice obtenue avec `mylu3b()` contient 3 valeurs différentes de 0, alors que la matrice obtenue avec `lu()` en contient 5. Cela est peut être dû au hasard.


    --> erreur = norm(A - c * d)
    erreur  = 

    2.532D-16

### 3.

`mylu.sci`
```Scilab
function [L,U] = mylu(A)

    [n,n] = size(A)

    for k = 1 : n - 1
        A(k+1:n,k) = A(k+1:n,k) / A(k,k)
        A(k+1:n,k+1:n) = A(k+1:n,k+1:n) - A(k+1:n,k) * A(k,k+1:n)
    end

    L = tril(A,-1)
    U = triu(A)

    for i = 1 : n
        L(i,i) = 1
    end

endfunction
```

### 4.

`mylu.sci`
``` Scilab
function [L,U,P] = mylu(A)

    [n,n] = size(A)
    P = zeros(1,n)
    for a = 1 : n
        P(1,a) = a
    end 


    for k = 1 : n - 1
        // pivot partiel
        [piv,ind] = max(abs(A(k : n,k)))
        ind = (k-1) + ind
        if ind ~= k then
            new = A(ind, :)
            A(ind, :) = A(k, :)
            A(k, :) = new
            q = P(1,ind)    
            P(1, ind) = P(1, k)
            P(1, k) = q
        end

        // LU
        A(k+1:n,k) = A(k+1:n,k) / A(k,k)
        A(k+1:n,k+1:n) = A(k+1:n,k+1:n) - A(k+1:n,k) * A(k,k+1:n)
    end

    L = tril(A,-1)
    U = triu(A)

    for i = 1 : n
        L(i,i) = 1
    end



endfunction
```

### 5.

    --> exec('/home/m5ssss/Desktop/calcul numerique/TD - TP2/mylu.sci',-1)

    --> A = rand(5,5)
    A  = 

    0.9003655   0.6896677   0.3695439   0.5194907   0.2589885
    0.1963      0.7311593   0.8033212   0.8672926   0.3345949
    0.029218    0.9265381   0.9033794   0.3814667   0.8190966
    0.0958223   0.3162372   0.3346502   0.5968302   0.5886622
    0.8838569   0.5837447   0.0631741   0.1801257   0.1522065

    -->[a,b,c] = lu(A)
    a  = 

    1.          0.          0.          0.          0.
    0.0324512   1.          0.          0.          0.
    0.9816646  -0.1031652   1.          0.          0.
    0.106426    0.26858    -0.2692835   1.          0.
    0.2180226   0.6423617  -0.7231926   0.8453421   1.
    
    b  = 

    0.9003655   0.6896677   0.3695439   0.5194907   0.2589885
    0.          0.9041576   0.8913872   0.3646086   0.8106921
    0.          0.         -0.2076338  -0.2922249  -0.0183981
    0.          0.          0.          0.3649249   0.3384092
    0.          0.          0.          0.         -0.5420049
 
    c  = 

    1.   0.   0.   0.   0.
    0.   0.   1.   0.   0.
    0.   0.   0.   0.   1.
    0.   0.   0.   1.   0.
    0.   1.   0.   0.   0.

    -->[d,e,f] = mylu(A)
    d  = 

    1.          0.          0.          0.          0.
    0.0324512   1.          0.          0.          0.
    0.9816646  -0.1031652   1.          0.          0.
    0.106426    0.26858    -0.2692835   1.          0.
    0.2180226   0.6423617  -0.7231926   0.8453421   1.
 
    e  = 

    0.9003655   0.6896677   0.3695439   0.5194907   0.2589885
    0.          0.9041576   0.8913872   0.3646086   0.8106921
    0.          0.         -0.2076338  -0.2922249  -0.0183981
    0.          0.          0.          0.3649249   0.3384092
    0.          0.          0.          0.         -0.5420049
    
    f  = 

    1.   3.   5.   4.   2.

Nous pouvons remarquer que le pivot obtenu avec `mylu()` correspond bien au pivot 2d obtenu avec `lu()`
