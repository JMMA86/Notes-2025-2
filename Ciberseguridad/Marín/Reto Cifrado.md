## Estudiante
- Juan Manuel Marín Angarita
- A00382037

## Solución del Reto
El archivo fue cifrado empleando el algoritmo AES en modalidad CTR. Como contraseña, se empleó la original respuesta que un concursante de “Quién quiere ser millonario?” diera a la pregunta “En los baños suelo estar, aunque provengo del mar”.

Primero se definió el Script que debería usarse para descifrar el primer archivo. Dado que se empleó el algoritmo AES en modalidad CTR, el comando podría ser:

```powershell
openssl enc -d --aes-128-ctr -in reto1.cif -out reto1.txt -k <password> -pbkdf2
```

La respuestas que tenía la pregunta en su momento eran:
- La esponja
- El espejo
- El tomacorriente
- La papelera

La respuesta que escogió fue la de "El tomacorriente", por lo que el comando queda:

```powershell
openssl enc -d --aes-128-ctr -in reto1.cif -out reto1.txt -k "tomacorriente" -pbkdf2
```

Sin embargo, esto no decodifica el archivo, por lo que se hará otro intento usando 192 bits:

```powershell
openssl enc -d --aes-192-ctr -in reto1.cif -out reto1.txt -k "tomacorriente" -pbkdf2
```

Esto sí descifra el primer archivo, arrojando el mensaje:

> [!RESPUESTA]
> Muy bien! Has descifrado la primera parte del reto!
> 
> El segundo archivo está cifrado con el algoritmo AES en modalidad CBC.
> 
> Clave: ffffeeeeddddccccbbbbaaaa99998888
> IV: 0123456789abcdeffedcba9876543210

Sigamos con el siguiente archivo. Dado que pide usar AES en modalidad CBC con las claves dadas, formaré el siguiente comando:

```powershell
openssl enc -d --aes-128-cbc -in reto2.cif -out reto2.txt -K ffffeeeeddddccccbbbbaaaa99998888 -iv 0123456789abcdeffedcba9876543210
```

Esto también descifra el segundo archivo, arrojando el mensaje:

> [!MENSAJE]
> Vas por buen camino... segunda parte resuelta!
> 
> El tercer archivo está cifrado con el algoritmo AES en modalidad CTR.
> 
> Clave: 0123456789abcdef0123456789abcdeffedcba9876543210fedcba9876543210
> IV: 11112222333344445555666677778888

Por último, realizaré el último comando siguiendo las indicaciones del mensaje:

```powershell
openssl enc -d --aes-128-ctr -in reto3.cif -out reto3.txt -K 0123456789abcdef0123456789abcdeffedcba9876543210fedcba9876543210 -iv 11112222333344445555666677778888
```

Sin embargo, eso arroja este error:

> [!ERROR]
> hex string is too long, ignoring excess

Entonces, probaremos con 192 bits:

```powershell
openssl enc -d --aes-192-ctr -in reto3.cif -out reto3.txt -K 0123456789abcdef0123456789abcdeffedcba9876543210fedcba9876543210 -iv 11112222333344445555666677778888
```

Tampoco funciona. Probaré con 256:

```powershell
openssl enc -d --aes-256-ctr -in reto3.cif -out reto3.txt -K 0123456789abcdef0123456789abcdeffedcba9876543210fedcba9876543210 -iv 11112222333344445555666677778888
```

Con esto, sí se descifra el tercer archivo, arrojando el mensaje:

> [!MENSAJE]
> Felicitaciones! Has completado el reto!!
> 
> "Un pesimista ve la dificultad en cada oportunidad,
>  un optimista ve la oportunidad en cada dificultad."
>          - Sir Winston Churchill

De esta forma, resolví el reto propuesto.