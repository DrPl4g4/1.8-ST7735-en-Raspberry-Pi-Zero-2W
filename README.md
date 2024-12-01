# 1. Esquema de conexiones entre la tft 1.8 de 160x128

![image](https://github.com/user-attachments/assets/9ffdbe03-16de-4281-bf89-b82b79ee1b1d)

# NO OVLIDES ACTIVAR EL SPI

# sudo raspi-config

![image](https://github.com/user-attachments/assets/e2989f8b-22d2-4e6c-ba2b-c174738a1eef)

![image](https://github.com/user-attachments/assets/f3b49b64-4089-4ef1-b303-1389e0855ddc)

![image](https://github.com/user-attachments/assets/ce549e16-6860-4769-8e77-7c33aa1afaec)



# 2. Descargar el archivo fuente: Asegúrate de que el archivo prajst77.dts esté disponible en tu directorio de trabajo. Si has clonado el repositorio, ya estará en la carpeta correspondiente.

git clone https://github.com/DrPl4g4/1.8-ST7735-en-Raspberry-Pi-Zero-2W.git

cd 1.8-ST7735-en-Raspberry-Pi-Zero-2W

# 3. Compilar el archivo DTS: Usa el comando dtc (Device Tree Compiler) para convertir manualmente el archivo prajst77.dts en su forma binaria prajst77.dtbo:

dtc -@ -I dts -O dtb -o prajst77.dtbo prajst77.dts

Verifica que se generó correctamente: Comprueba que el archivo binario se creó correctamente:

ls | grep prajst77.dtbo

Si ves el archivo prajst77.dtbo listado, la compilación fue exitosa.

# 4. Mover el archivo al directorio de overlays: Copia el archivo generado al directorio /boot/overlays/, donde se almacenan todos los overlays del sistema:

sudo cp prajst77.dtbo /boot/overlays/

Confirmar que el archivo está en el directorio correcto: Asegúrate de que el archivo está en el lugar adecuado:

ls /boot/overlays/ | grep prajst77

# 5. Habilitar el overlay en config.txt: Edita el archivo de configuración de la Raspberry Pi para activar el overlay:

sudo nano /boot/config.txt

# Añade esta línea al final del archivo:

#Overlay del framebuffer personalizado
dtoverlay=prajst77,debug=3

#Configuración del framebuffer
framebuffer_width=128       # Ancho de la pantalla ST7735
framebuffer_height=160      # Alto de la pantalla ST7735
framebuffer_depth=16        # Profundidad de color (16 bits recomendado para ST>
framebuffer_ignore_alpha=1  # Ignorar canal alfa

#Deshabilitar HDMI si no lo usas
hdmi_force_hotplug=1        # Forzar salida HDMI (útil para pantallas no HDMI)
hdmi_group=2                # Grupo de modo (2: DMT - para monitores)
hdmi_mode=87                # Modo definido por el usuario
hdmi_cvt=128 160 60 1 0 0 0 # Resolución personalizada: 128x160, 60Hz
