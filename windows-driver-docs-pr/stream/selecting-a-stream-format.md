---
title: ストリーム形式の選択
description: ストリーム形式の選択
ms.assetid: 876eca52-4d5e-45bd-90df-ff4b6405078d
keywords:
- ビデオキャプチャ WDK AVStream、ストリーム形式
- ビデオのキャプチャ WDK AVStream、ストリーム形式
- ストリーミング形式 WDK ビデオキャプチャ
- WDK ビデオキャプチャのフォーマット
- データの共通部分の実行 WDK ビデオキャプチャ
- データの共通部分 (WDK ビデオキャプチャ)
- WDK ビデオキャプチャの共通部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d464f3604888513a92bbc3d45c865cd74475f36c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843322"
---
# <a name="selecting-a-stream-format"></a>ストリーム形式の選択


ビデオキャプチャデバイスは、さまざまな形式でビデオをキャプチャできます。 [**Ksk datarの**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造は、特定の色空間の幅、高さ、粒度、トリミング、およびフレームレートに関する情報を伝えるために使用されます。 [ **\_video**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)および[**KS\_DATARANGE\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2)の構造\_体は、ksdatarange 構造体の拡張機能であり、ビデオキャプチャ形式を記述するために使用する必要があります。 ビデオフレームのみを記述するには、KS\_DATARANGE\_ビデオを使用します。 VIDEO2 を\_\_使用して、ビデオフィールドとビデオフレームを記述します。これには、bob またはの設定の有無は関係ありません。

ストリーム形式を選択するプロセスは、*データ積集合の実行*と呼ばれます。 ストリームクラスインターフェイスは、データの積集合を実行するために、ストリームクラスミニドライバーに[ **\_データ\_共通部分要求\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection)を送信します。 ミニドライバーは、要求されたデータ範囲の有効性を判断し、指定されたデータ範囲から特定のストリーム形式を選択します。通常は、 [**ks\_DATAFORMAT\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader)または ks を使用し[ **\_DATAFORMAT\_VIDEOINFOHEADER2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader2)構造体。

最後に、ミニドライバーは、次に示すように、結果の形式の特定のメンバーを設定する必要があります。

```cpp
.
.
.
// Calculate biSizeImage for this request, and put the result in both
// the biSizeImage field of the bmiHeader AND in the SampleSize field
// of the DataFormat.
//
// Note that for compressed sizes, this calculation will probably not
// be just width * height * bitdepth
 
DataFormatVideoInfoHeaderOut->VideoInfoHeader.bmiHeader.biSizeImage =
DataFormatVideoInfoHeaderOut->DataFormat.SampleSize = 
KS_DIBSIZE(DataFormatVideoInfoHeaderOut->VideoInfoHeader.bmiHeader);
.
.
```

 

 




