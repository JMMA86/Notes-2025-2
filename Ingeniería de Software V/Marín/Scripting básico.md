## 1. Estructura General

|Aspecto|PowerShell|Bash|
|---|---|---|
|Extensión|`.ps1`|`.sh`|
|Ejecución|`.\script.ps1`|`bash script.sh` o `./script.sh`|
|Comentarios|`# Comentario`|`# Comentario`|

## 2. Estructuras de Control

#### 🧭 Condicional `if`

**PowerShell:**

```powershell
if ($x -eq 5) {
    Write-Host "Es 5"
} elseif ($x -lt 5) {
    Write-Host "Menor"
} else {
    Write-Host "Mayor"
}
```

**Bash:**

```bash
if [ "$x" -eq 5 ]; then
    echo "Es 5"
elif [ "$x" -lt 5 ]; then
    echo "Menor"
else
    echo "Mayor"
fi
```

#### Bucles

**For**

- PowerShell:
    

```powershell
for ($i = 0; $i -lt 5; $i++) {
    Write-Host $i
}
```

- Bash:
    

```bash
for ((i = 0; i < 5; i++)); do
    echo $i
done
```

**While**

- PowerShell:
    

```powershell
while ($i -lt 5) {
    Write-Host $i
    $i++
}
```

- Bash:
    

```bash
while [ $i -lt 5 ]; do
    echo $i
    ((i++))
done
```

---

## 3. Variables

|PowerShell|Bash|
|---|---|---|
|Declaración|`$nombre = "Juan"`|`nombre="Juan"`|
|Uso|`$nombre`|`$nombre`|

## 4. Funciones

**PowerShell:**

```powershell
function Saludar($nombre) {
    Write-Host "Hola $nombre"
}
```

**Bash:**

```bash
saludar() {
    echo "Hola $1"
}
```

## 5. Comandos Comunes

|Tarea|PowerShell|Bash|
|---|---|---|
|Imprimir|`Write-Host`|`echo`|
|Listar files|`Get-ChildItem`|`ls`|
|Cambiar dir|`Set-Location`|`cd`|
|Eliminar file|`Remove-Item`|`rm`|
