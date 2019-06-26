---
title: WIA 未処理形式のデータ ヘッダー
description: WIA 未処理形式のデータ ヘッダー
ms.assetid: a2cb3835-7879-4f69-9784-9487df40730a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 458552ca5d8b4362de397e03ce971f5f9a26f05a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355164"
---
# <a name="wia-raw-data-header"></a>WIA 未処理形式のデータ ヘッダー


生データのヘッダーは次のとおりです。

```cpp
DWORD Tag;         // must contain 'WRAW' (single byte ASCII characters)
DWORD Version;        // must contain 0x00010000
DWORD HeaderSize;       // contains amount of valid bytes in header
DWORD XRes;              // X (horizontal) resolution, in DPI
DWORD YRes;              // Y (vertical) resolution, in DPI
DWORD XExtent;           // image width, in pixels
DWORD YExtent;           // image height, in pixels
DWORD BytesPerLine;      // used only for uncompressed image data, 0 (unknown) for compressed data 
DWORD BitsPerPixel;      // number of bits per pixel (all channels)
DWORD ChannelsPerPixel;  // number of color channels (samples) within a pixel
DWORD DataType;    // current WIA_IPA_DATATYPE value describing the image
BYTE  BitsPerChannel[8]; // up to 8 channels per pixel, use as many as needed  
DWORD Compression;       // current WIA_IPA_COMPRESSION value
DWORD PhotometricInterp; // current WIA_IPS_PHOTOMETRIC_INTERP value
DWORD LineOrder;         // image line order as a WIA_LINE_ORDER value
DWORD RawDataOffset;     // offset position (in bytes, starting from 0) for the raw image data
DWORD RawDataSize;       // size of raw image data, in bytes
DWORD PaletteOffset;     // offset position (in bytes, starting from 0) for the palette (0 if none)
DWORD PaletteSize;       // size, in bytes, of color palette table (0 if no palette is required) 
```

### <a name="additional-header-field-descriptions"></a>追加のヘッダー フィールドの説明

<a href="" id="dword-compression"></a>DWORD*圧縮*  
同社の圧縮 NEF headerless の圧縮されたデータが圧縮された fax の転送 (グループ 3.1、3.2d, 4) の使用など、圧縮された生の形式を使用できます。 値をこのフィールドは WIA\_IPA\_圧縮定数、可能性があるベンダー固有の特殊化されたアプリケーション。 既定値は WIA\_圧縮\_NONE。

圧縮の例:

G4 圧縮されたデータ (WIA\_圧縮\_G4) 可能性があります、TIFF ファイル内のいずれかを転送 (WiaImgFmt\_TIFF) または未加工の形式を使用して (WiaImgFmt\_RAW)。

JPEG 圧縮されたデータ (WIA\_圧縮\_JPEG) JFIF 形式を使用して転送する可能性があります (WiaImgFmt\_JPEG)、EEXIF 形式 (WiaImgFmt\_EXIF)、または TIFF 形式 (WiaImgFmt\_TIFF). インターチェンジの形式 (JFIF、EEXIF) 生の形式を使用して転送内のいずれかで書式設定された JPEG データを転送することはできません (WiaImgFmt\_RAW)-その他の JPEG と互換性のある形式のいずれかを使用する必要は代わりに、します。

WIA 圧縮の定数の詳細については、次を参照してください。、 [ **WIA\_IPA\_圧縮**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-compression)プロパティ。

<a href="" id="dword-photometricinterp"></a>DWORD *PhotometricInterp*  
転送されるイメージのメトリックスをについて説明します。 このフィールドは、黒と白 (1bpp) と (4 bpp 以上)、グレースケール イメージに必要です。 これらのイメージは白と黒、WIA のどちらかの値を指定する必要があります\_写真\_白\_1 (位置 0 は黒、白の 1 の場合) または WIA\_写真\_白い\_0 (場所白は 0、1 を黒には)。 このフィールドは、カラー イメージでは省略可能です。

<a href="" id="dword-lineorder"></a>DWORD *LineOrder*  
上から下または下から上にイメージ データの行/行は順序付けするかどうかについて説明します。 定義された 2 つの新しい定数*wiadef.h*この。

```cpp
#define  WIA_LINE_ORDER_TOP_TO_BOTTOM        0x00000001 
#define  WIA_LINE_ORDER_BOTTOM_TO_TOP        0x00000002
```

これで定義された新しいプロパティはありません。 これは、構成可能なスキャンの設定はありません。 *LingOrder*だけで実行するときに重要なデータ転送のイメージします。

<a href="" id="dword-rawdatasize"></a>DWORD *RawDataSize*  
(省略可能なカラー パレットを含まない) ヘッダーの後の生データのバイト単位のサイズを示します。 アプリケーションは、このフィールドを使用して、成功したイメージを前提となる転送の完了を確認する可能性があります。 この情報がない場合ミニドライバーに既知時に、転送の開始 (し、ヘッダーは、ストリームに書き込まれます) の例では罫線を自動検出を使用して、イメージがスキャンされる場合、ミニドライバーは、i の最後に、このフィールドに入力する必要があります。mage データ転送、XExtent と YExtent フィールドの処理方法に似ています。

<a href="" id="dword-paletteoffset"></a>DWORD *PaletteOffset*  
データ ストリーム内のカラー パレットの開始位置のバイト オフセットが含まれていますこのオフセットが (位置 0) から開始し、ヘッダーが終了する. パレットとイメージの生データは、任意の順序で生のヘッダーをフォローでき、必要ない場合にパレットを省略できます。

<a href="" id="dword-palettesize"></a>DWORD *PaletteSize*  
カラー パレットのバイト単位のサイズが含まれています。 パレットする未処理のイメージ データに接続する必要がない場合、ミニドライバーは、0 にこのフィールドを設定する必要があります。 このフィールドは、パレット内のエントリの数とは無関係です。

黒と白とグレースケール データは、パレットを省略できます (にパレットのビルドに必要な情報が含まれているため、 *PhotometricInterpretation*フィールド) と共に最適化のパレットを指定しますまたは、  *。PhotometricInterpretation*フィールド。

インデックス付きのイメージのカラー パレット内のエントリの数は、現在によって異なります*BitsPerPixel*値 (2 ^ *BitsPerPixel*します。 たとえば、1bpp、4 bpp の 16 個のエントリ、256 エントリ 8bpp の 2 つのエントリを使用)。 パレット エントリの形式は、エントリの数によって決まるよう*BitsPerChannel*フィールド (パレットの各エントリのフィールド/チャンネル数) と*BitsPerChannel* (各フィールドは値指定された値だけを含めることが、 *BitsPerChannel*それぞれチャネルのフィールド)。 パレットの各エントリ フィールドは、バイト境界で配置にある必要があります。

 

 




