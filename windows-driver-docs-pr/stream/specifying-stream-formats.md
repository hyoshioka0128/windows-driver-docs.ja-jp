---
title: ストリーム形式の指定
description: ストリーム形式の指定
ms.assetid: 60ef129c-f4a1-4eb5-97d9-6be6c7803258
keywords:
- ビデオキャプチャ WDK AVStream、ストリーム形式
- ビデオのキャプチャ WDK AVStream、ストリーム形式
- ストリーミング形式 WDK ビデオキャプチャ
- WDK ビデオキャプチャのフォーマット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c93d5803bbf09dbd42a51d6198110db2a1d300f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843317"
---
# <a name="specifying-stream-formats"></a>ストリーム形式の指定


一般に、DirectShow およびカーネルストリーミングは、メディア形式の定義とストリーミングの規則を共有します。 この統一性は、カーネルモードとユーザーモードのコンポーネントで使用される名前付け規則の違いによって若干隠されています。 カーネルモードで使用される多くのメディア形式と GUID 定義にはプレフィックス*KS\_* がありますが、それ以外の場合はユーザーモードと同じです。 たとえば、カーネルモード構造 ( [**KS\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)) の Win32 ユーザーモードバージョンは、bitmapinfoheader です。

ビデオキャプチャミニドライバーは、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体を使用して特定のストリーム形式を記述します。 ただし、ミニドライバーでは、 [**ksk**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))の型の配列を指定することによって、潜在的なストリーム形式を広範囲に公開することもできます。 KSK DATARの構造体は、色の形式、ビット深度、トリミング、スケーリングの可能性などのイメージ特性を記述します。

1つの KSDATARANGE 構造体は、何千もの潜在的な構造を記述できます。 たとえば、KSDATARANGE 構造体では、最小次元が160x120 ピクセルで、最大次元が 720 x 480 ピクセルであるサンプルのビデオストリームを指定できます。これにより、x ディメンションと y 次元で粒度ステップサイズ値が1になります。 これにより、アプリケーションは、一意の KSDATAFORMAT 構造体を使用して、20万を超える出力イメージのディメンションを要求できます。

DirectShow は、KSDATAFORMAT に似た構造を使用して、ストリーム形式を定義します。 次に、例を示します。

```cpp
typedef struct  _AMMediaType    {
    GUID majortype;            // Same as KSDATAFORMAT.MajorFormat
    GUID subtype;              // Same as KSDATAFORMAT.SubFormat
    BOOL bFixedSizeSamples;
    BOOL bTemporalCompression;
    ULONG lSampleSize;         // Same as KSDATAFORMAT.SampleSize
    GUID formattype;           // Same as KSDATAFORMAT.Specifier
    IUnknown __RPC_FAR *pUnk;
    ULONG cbFormat;
    BYTE *pbFormat;
 } AM_MEDIA_TYPE;
```

名前付け規則の違いにかかわらず、カーネルモード KSK の KSDATAFORMAT/とユーザーモード\_\_AM の両方で使用される Guid は同じです。

**注**  : KSDATAFORMAT 構造体の**subformat**メンバーの下位4バイト (AM\_メディア\_TYPE ユーザーモード構造の**サブタイプ**メンバーに似ています) は、使用されている FOURCC 値と一致している必要があります[**KS\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)構造体の**biCompression**メンバー。 これらのバイトは、形式を逆の順序で記述する16進 ASCII 文字を保持します。

たとえば、次の GUID は、YVU9 FOURCC ビデオ形式に対応しています。

```Text
39555659-0000-0010-8000-00AA00389B71
      59 = 'Y'
    56 = 'V'
  55 = 'U'
39 = '9'
```
