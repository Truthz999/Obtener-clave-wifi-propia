# # Obtener Clave Wifi de la red en la que estas sin tener que ir al rooter
**Solo funciona con redes wifi donde tu estes conectado y se puede hacer exactamente lo mismo en cmd solo que lo automatizas en un script**

# Code

```python

import subprocess
import os

perfil_red = input('Introduce el nombre de la red Wifi: ')

try:

    resultados = subprocess.check_output(['netsh' , 'wlan' , 'show' , 'profile' , perfil_red, 'key=clear'], shell= True).decode('utf-8' , errors= 'backslashreplace')

    # Si el sistema es en ingles se pondra 'Key Content' en vez de 'Contenido de la clave'
    if 'Contenido de la clave' in resultados:
        print(resultados)
        for line in resultados.split('\n'):
            if 'Contenido de la clave' in line:
                password = line.split(':')[1].strip()
                print(f'La contraseña de la red {perfil_red} es: \x1b[1;33m {password}')
                break

    else:
        print(f'No se encontro la contraseña para la red {perfil_red}')

except subprocess.CalledProcessError:
    print(f'No se encontro la informacion del perfil {perfil_red}')


```


