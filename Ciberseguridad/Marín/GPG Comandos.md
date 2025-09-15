Listar claves públicas:

```powershell
gpg --list-keys
```

Listar claves privadas:

```powershell
gpg --list-secret-keys
```

Crear clave pública:

```powershell
gpg --full-gen-key
```

Exportar clave:

```powershell
gpg --export -a > claveMarinJuan.txt
```

Importar clave:

```powershell
gpg --import claveMarinJuan.txt
```

Encriptar archivo:

```powershell
gpg --encrypt -a -r os.gomez.lozano@gmail.com jmmm.txt
```

Desencriptar:

```powershell
gpg --decrypt mensaje.txt.asc
```

Firmar:

```powershell
gpg --sign --clearsign jmmm.txt
```

Comprobar firma:

```powershell
gpg --verify MensajeFirmado.txt.asc
```

Editar confianza:

```powershell
gpg --edit-key jcuellar@icesi.edu.co
trust
s
save
```

Crear Firma:

```powershell
gpg --sign --detach-sign -a GuiaGPG.pdf
```

Comparar Hashes:

```powershell
fc hash1.txt hash2.txt
```

