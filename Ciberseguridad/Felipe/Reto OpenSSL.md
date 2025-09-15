
# Reto 1
Bueno en primera instancia se nos pasa el reto1.cif por el cual es codificado con las siguientes instrucciones:

```
El archivo fue cifrado empleando el algoritmo AES en modalidad CTR. Como contraseña, se empleó la original respuesta que un concursante de “Quién quiere ser millonario?” diera a la pregunta “En los baños suelo estar, aunque provengo del mar”.
```

Primero es investigar cual seria la clave y buscando por internet busque la pista de ese concurso de quien quiere ser millonario:

[El concursante de Quién Quiere ser Millonario más penca que jamás verás en tu vida](https://www.theclinic.cl/2013/12/03/el-concursante-de-quien-quiere-ser-millonario-mas-penca-que-jamas-veras-en-tu-vida/)

Entonces con los comandos vistos en clase intente primero :
```Openssl
openssl enc -aes-128-ctr -d -in reto1.cif -out reto1_128_pbkdf2.txt -k "Eltomacorriente"

openssl enc -aes-128-ctr -d -in reto1.cif -out reto1_128_pbkdf2.txt -k "ELTOMACORRIENTE"

openssl enc -aes-128-ctr -d -in reto1.cif -out reto1_128_pbkdf2.txt -k "eltomacorriente"
```

Y todas las otras posibles, pero recordemos que cuando le damos **openssl** el nos muestra:

![[Pasted image 20250813084938.png]]

Los comandos de cifrado y la pista nos dice que esta en AES con modalidad CTR entonces probé con 128, 256, 192 hasta que que claramente me dio:

```Openssl
openssl enc -aes-192-ctr -d -pbkdf2 -in reto1.cif -out reto1.txt -k "tomacorriente"
```

![[Pasted image 20250813085229.png]]
Con esto también me di cuenta de varias cosas de como se debe pasar el parámetro con comillas o sin comillas, ya que influiría si la contraseña fuera "El tomacorriente" por ese espacio solamente tomaría "El" y no toda la frase.

# Reto 2

![[Pasted image 20250813085701.png]]


Aqui las instrucciones son claras usar algoritmo AEST con modalidad CBC y ya me estan pasando la clave entonces solamente sigo los pasos y le paso la clave y el iv. Ademas recordemos que:

- **AES-128** usa una clave de **128 bits** $\to$ 16 bytes (32 caracteres hexadecimales).
- **AES-192** usa una clave de **192 bits** $\to$ 24 bytes (48 caracteres hexadecimales).
- **AES-256** usa una clave de **256 bits** $\to$ 32 bytes (64 caracteres hexadecimales).

```Openssl
openssl enc -aes-128-cbc -d -in reto2.cif -out reto2.txt -K ffffeeeeddddccccbbbbaaaa99998888 -iv 0123456789abcdeffedcba9876543210
```

![[Pasted image 20250813095927.png]]

Esta parte fue un poco mas sencilla que la primera por lo que solamente faltaria poder completar el reto 3.


# Reto 3

Siguiendo las instrucciones de la segunda pista:

![[Pasted image 20250813100430.png]]


Me dicen que esta cifrado con AES en modalidad CTR entonces recordemos:

- **AES-128** usa una clave de **128 bits** $\to$ 16 bytes (32 caracteres hexadecimales).
- **AES-192** usa una clave de **192 bits** $\to$ 24 bytes (48 caracteres hexadecimales).
- **AES-256** usa una clave de **256 bits** $\to$ 32 bytes (64 caracteres hexadecimales).


Entonces ya podemos decifrar el reto 3 que seria:

```Openssl
openssl enc -aes-256-ctr -d -in reto3.cif -out reto3.txt -K 0123456789abcdef0123456789abcdeffedcba9876543210fedcba9876543210 -iv 11112222333344445555666677778888
```
![[Pasted image 20250813120420.png]]

# Conclusiones

El reto de descifrado con **OpenSSL** resultó no solo una práctica técnica valiosa, sino también una experiencia divertida y entretenida. A través de la identificación del algoritmo **AES en modo CTR** y el análisis de la longitud de la clave e IV, se reforzaron conocimientos fundamentales sobre criptografía simétrica, manejo de bits y formatos hexadecimales. Además, permitió aplicar el razonamiento lógico para deducir el tipo de AES utilizado, afianzando la capacidad de **análisis y resolución de problemas**. En resumen, la actividad combinó aprendizaje técnico con el gusto de experimentar y descubrir lo visto en clase.