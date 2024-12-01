Descargar el archivo fuente: Asegúrate de que el archivo prajst77.dts esté disponible en tu directorio de trabajo. Si has clonado el repositorio, ya estará en la carpeta correspondiente.

git clone https://github.com/DrPl4g4/1.8-ST7735-en-Raspberry-Pi-Zero-2W.git

cd 1.8-ST7735-en-Raspberry-Pi-Zero-2W

Compilar el archivo DTS: Usa el comando dtc (Device Tree Compiler) para convertir manualmente el archivo prajst77.dts en su forma binaria prajst77.dtbo:

dtc -@ -I dts -O dtb -o prajst77.dtbo prajst77.dts

Verifica que se generó correctamente: Comprueba que el archivo binario se creó correctamente:

ls | grep prajst77.dtbo
