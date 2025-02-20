This is a barcode generation package inspired by [https://github.com/tecnickcom/TCPDF](https://github.com/tecnickcom/TCPDF). Actually I use that package's underline classes for generating barcode. This package is just a wrapper of that package and adds compatibility with Laravel 5.

I used the following classes of that package.

- src/Milon/Barcode/Datamatrix.php (include/barcodes/datamatrix.php)
- src/Milon/Barcode/DNS1D.php (tcpdf_barcodes_1d.php)
- src/Milon/Barcode/DNS2D.php (tcpdf_barcodes_2d.php)
- src/Milon/Barcode/PDF417.php (include/barcodes/pdf417.php)
- src/Milon/Barcode/QRcode.php (include/barcodes/qrcode.php)

[Read More on TCPDF website](http://www.tcpdf.org)

## Installation

Begin by installing this package through Composer. Edit your project's `composer.json` file to require `milon/barcode`.

    "require": {
		...
		"milon/barcode": "dev-master"
	}

Next, update Composer from the Terminal:

    composer update

Once this operation completes, the final step is to add the service provider. Open `config/app.php`, and add a new item to the providers array.

    'Milon\Barcode\BarcodeServiceProvider'

If you want to change Bar-code's settings (Store Path etc.), you need to publish its config file(s). For that you need to run in the terminal-

    php artisan vendor:publish

Make sure you have write permission to the storage path. By default it sets to `/storage` folder.

Now add the alias.

```php
'aliases' => [
	...
	'DNS1D' => 'Milon\Barcode\Facades\DNS1DFacade',
	'DNS2D' => 'Milon\Barcode\Facades\DNS2DFacade',
]
```

Bar-code generator like 
Qr Code,
PDF417,
C39,C39+,
C39E,C39E+,
C93,
S25,S25+,
I25,I25+,
C128,C128A,C128B,C128C,
2-Digits UPC-Based Extention,
5-Digits UPC-Based Extention,
EAN 8,EAN 13,
UPC-A,UPC-E,
MSI (Variation of Plessey code)

generator in html, png embedded base64 code and SVG canvas 

```php
echo DNS1D::getBarcodeSVG("4445645656", "PHARMA2T");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T");
echo '<img src="data:image/png,' . DNS1D::getBarcodePNG("4", "C39+") . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath("4445645656", "PHARMA2T");
echo '<img src="data:image/png,' . DNS1D::getBarcodePNG("4", "C39+") . '" alt="barcode"   />';
```

```php
echo DNS1D::getBarcodeSVG("4445645656", "C39");
echo DNS2D::getBarcodeHTML("4445645656", "QRCODE");
echo DNS2D::getBarcodePNGPath("4445645656", "PDF417");
echo DNS2D::getBarcodeSVG("4445645656", "DATAMATRIX");
echo '<img src="data:image/png,' . DNS2D::getBarcodePNG("4", "PDF417") . '" alt="barcode"   />';
```

## Width and Height example

```php
echo DNS1D::getBarcodeSVG("4445645656", "PHARMA2T",3,33);
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T",3,33);
echo '<img src="' . DNS1D::getBarcodePNG("4", "C39+",3,33) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath("4445645656", "PHARMA2T",3,33);
echo '<img src="data:image/png,' . DNS1D::getBarcodePNG("4", "C39+",3,33) . '" alt="barcode"   />';
```
    
## Color

```php
echo DNS1D::getBarcodeSVG("4445645656", "PHARMA2T",3,33,"green");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T",3,33,"green");
echo '<img src="' . DNS1D::getBarcodePNG("4", "C39+",3,33,array(1,1,1)) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath("4445645656", "PHARMA2T",3,33,array(255,255,0));
echo '<img src="data:image/png,' . DNS1D::getBarcodePNG("4", "C39+",3,33,array(1,1,1)) . '" alt="barcode"   />';
```

## 2D Barcodes

```php
echo DNS2D::getBarcodeHTML("4445645656", "QRCODE");
echo DNS2D::getBarcodePNGPath("4445645656", "PDF417");
echo DNS2D::getBarcodeSVG("4445645656", "DATAMATRIX");
```

## 1D Barcodes

```php
echo DNS1D::getBarcodeHTML("4445645656", "C39");
echo DNS1D::getBarcodeHTML("4445645656", "C39+");
echo DNS1D::getBarcodeHTML("4445645656", "C39E");
echo DNS1D::getBarcodeHTML("4445645656", "C39E+");
echo DNS1D::getBarcodeHTML("4445645656", "C93");
echo DNS1D::getBarcodeHTML("4445645656", "S25");
echo DNS1D::getBarcodeHTML("4445645656", "S25+");
echo DNS1D::getBarcodeHTML("4445645656", "I25");
echo DNS1D::getBarcodeHTML("4445645656", "I25+");
echo DNS1D::getBarcodeHTML("4445645656", "C128");
echo DNS1D::getBarcodeHTML("4445645656", "C128A");
echo DNS1D::getBarcodeHTML("4445645656", "C128B");
echo DNS1D::getBarcodeHTML("4445645656", "C128C");
echo DNS1D::getBarcodeHTML("44455656", "EAN2");
echo DNS1D::getBarcodeHTML("4445656", "EAN5");
echo DNS1D::getBarcodeHTML("4445", "EAN8");
echo DNS1D::getBarcodeHTML("4445", "EAN13");
echo DNS1D::getBarcodeHTML("4445645656", "UPCA");
echo DNS1D::getBarcodeHTML("4445645656", "UPCE");
echo DNS1D::getBarcodeHTML("4445645656", "MSI");
echo DNS1D::getBarcodeHTML("4445645656", "MSI+");
echo DNS1D::getBarcodeHTML("4445645656", "POSTNET");
echo DNS1D::getBarcodeHTML("4445645656", "PLANET");
echo DNS1D::getBarcodeHTML("4445645656", "RMS4CC");
echo DNS1D::getBarcodeHTML("4445645656", "KIX");
echo DNS1D::getBarcodeHTML("4445645656", "IMB");
echo DNS1D::getBarcodeHTML("4445645656", "CODABAR");
echo DNS1D::getBarcodeHTML("4445645656", "CODE11");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T");
```

## License
This package is published under `GNU LGPLv3` license and copyright to [Nuruzzaman Milon](http://milon.im). Original Barcode generation classes were written by Nicola Asuni. The license agreement is on project's root.

License: GNU LGPLv3   
Package Author: [Nuruzzaman Milon](http://milon.im)   
Original Barcode Class Author: [Nicola Asuni](http://www.tcpdf.org)   
Package Copyright: Nuruzzaman Milon   
Barcode Generation Class Copyright:   
Nicola Asuni   
Tecnick.com LTD   
www.tecnick.com   