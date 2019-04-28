---
title: ストリーム形式の指定
description: ストリーム形式の指定
ms.assetid: 60ef129c-f4a1-4eb5-97d9-6be6c7803258
keywords:
- ビデオ キャプチャ WDK AVStream、stream の形式
- ビデオの WDK AVStream をキャプチャするには、ストリームを形式します。
- ストリーム形式 WDK のビデオのキャプチャ
- WDK のビデオ キャプチャを書式設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9438d9c0151e83b5f9bdd035c5184af76a3e9eb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360820"
---
# <a name="specifying-stream-formats"></a>ストリーム形式の指定


一般に、DirectShow とストリーミング メディアを共有カーネルは、定義とストリーミングの規則をフォーマットします。 この統一性は、カーネル モードとユーザー モード コンポーネントによって使用される名前付け規則の違いによって多少隠されています。 多くのメディアをフォーマットし、カーネル モードで使用される GUID の定義は、プレフィックスを付ける*KS\_* は対応するユーザー モードと同じです。 カーネル モード構造体の Win32 ユーザー モードのバージョンなど、 [ **KS\_BITMAPINFOHEADER**](https://msdn.microsoft.com/library/windows/hardware/ff567305)、BITMAPINFOHEADER です。

ビデオ キャプチャ ミニドライバーを使用して特定のストリーム形式について説明します、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)構造体。 ただし、ミニドライバーも公開できます潜在的なストリームの形式の広い範囲の配列を指定することによって[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。 KSDATARANGE 構造体には、色の書式、ビットの深さのトリミングおよびスケーリングの可能性などのイメージの特性について説明します。

1 つの KSDATARANGE 構造は、何千もの潜在的な KSDATAFORMAT 構造を記述できます。 たとえば、KSDATARANGE 構造では、160 x 120 ピクセルの最小の寸法と 720 x 480 (ピクセル単位) のステップ実行のサイズ値 x 1 の粒度の最大次元と y ディメンション RGB24 サンプルのビデオ ストリームを指定できます。 これにより、一意 KSDATAFORMAT 構造での 200,000 台を超えるの可能な出力画像のサイズのいずれかのアプリケーションが要求する可能性があります。

DirectShow では、KSDATAFORMAT と同様の構造を使用して、stream の形式を定義します。 次に、例を示します。

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

いるにもかかわらず、カーネル モード KSDATARANGE/KSDATAFORMAT とユーザー モードの両方で使用される Guid の名前付け規則の違いは\_メディア\_型の構造体は同じです。

**注**  :下位の 4 バイト、**サブフォーマット**KSDATAFORMAT 構造体のメンバー (に似ていますが、**サブタイプ**AM のメンバー\_メディア\_型ユーザー モードの構造体)使用される FOURCC 値と一致する必要があります、 **biCompression**のメンバー、 [ **KS\_BITMAPINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567305)構造体。 これらのバイトは、逆の順序で、形式を表す 16 進数の ASCII 文字を保持します。

たとえば、次の GUID は YVU9 FOURCC ビデオ形式に対応します。

```Text
39555659-0000-0010-8000-00AA00389B71
      59 = 'Y'
    56 = 'V'
  55 = 'U'
39 = '9'
```
