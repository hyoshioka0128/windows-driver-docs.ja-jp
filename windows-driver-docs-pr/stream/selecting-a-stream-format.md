---
title: ストリーム形式の選択
description: ストリーム形式の選択
ms.assetid: 876eca52-4d5e-45bd-90df-ff4b6405078d
keywords:
- ビデオ キャプチャ WDK AVStream、stream の形式
- ビデオの WDK AVStream をキャプチャするには、ストリームを形式します。
- ストリーム形式 WDK のビデオのキャプチャ
- WDK のビデオ キャプチャを書式設定します。
- パフォーマンス データの交差部分 WDK ビデオのキャプチャします。
- データの交差部分を WDK のビデオのキャプチャします。
- 交差部分を WDK のビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d791905e9957cf986915ba8933bd4d4f155398f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358411"
---
# <a name="selecting-a-stream-format"></a>ストリーム形式の選択


ビデオ キャプチャ デバイスには、さまざまな異なる形式でビデオをキャプチャできます。 [ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造を使用して、幅、高さ、粒度、トリミング、に関する情報を伝達し、フレーム レート、特定のカラー スペースをします。 構造体[ **KS\_DATARANGE\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video)と[ **KS\_DATARANGE\_VIDEO2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video2) KSDATARANGE 構造の拡張機能は、ビデオのキャプチャの形式を記述するために使用する必要があります。 使用 KS\_DATARANGE\_ビデオ フレームのみを説明するビデオです。 使用 KS\_DATARANGE\_VIDEO2 ビデオ フィールドとビデオのフレーム、bob の有無について説明します、設定を一元管理したりします。

ストリームの形式を選択するプロセスが呼び出されます*データの交差部分を実行する*します。 Stream クラス インターフェイスの送信、 [ **SRB\_取得\_データ\_交差**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection) Stream クラスのミニドライバーに要求データの積集合を実行します。 ミニドライバーは、通常を使用して要求されたデータ範囲の有効性を判断して、提供されたデータ範囲からの特定のストリームの形式を選択を担当[ **KS\_DATAFORMAT\_VIDEOINFOHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader)または[ **KS\_DATAFORMAT\_VIDEOINFOHEADER2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader2)構造体。

最後に、次に示すよう、ミニドライバーは結果の形式の特定のメンバーを設定する必要があります。

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

 

 




