This is a port of Nayuki's QR-Code-generator from https://github.com/nayuki/QR-Code-generator/tree/master/c
it has been made into a library for the Microchip PIC32MX but would work on any pic with a spare 1.8K data 
memory to spare. 
I use this calling method:
bool ok = qrcodegen_encodeText(text, tempBuffer, qrcode, qrcodegen_Ecc_MEDIUM,	qrcodegen_VERSION_MIN,
        qrcodegen_VERSION_MAX, qrcodegen_Mask_AUTO, true);
	if (ok)
    {
        printQr(qrcode);
    }

printQr(qrcode) is modified from Nayuki's:

/*---- Utilities ----*/

// Prints the given QR Code to the console.
static void printQr(const uint8_t qrcode[]) {
	int size = qrcodegen_getSize(qrcode);
	int border = 4;
	for (int y = -border; y < size + border; y++) {
		for (int x = -border; x < size + border; x++) {
			fputs((qrcodegen_getModule(qrcode, x, y) ? "##" : "  "), stdout);
		}
		fputs("\n", stdout);
	}
	fputs("\n", stdout);
}

I use the modified version to create an xpm which I then display on a 128x32 display.
