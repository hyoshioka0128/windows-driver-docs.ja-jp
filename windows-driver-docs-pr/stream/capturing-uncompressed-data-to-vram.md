---
title: 圧縮されていないデータの VRAM へのキャプチャ
description: 圧縮されていないデータの VRAM へのキャプチャ
ms.assetid: efec607d-3337-40a5-812c-57292f201d54
keywords:
- VRAM キャプチャ WDK AVStream、非圧縮データ
- 非圧縮データ WDK VRAM キャプチャ
- WDK VRAM キャプチャの形式
- 固定 VRAM 処理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bfad465f52cb814a8259c373ea7dc878463460d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844752"
---
# <a name="capturing-uncompressed-data-to-vram"></a>圧縮されていないデータの VRAM へのキャプチャ


VRAM が有効になっている AVStream ミニドライバーは、キャプチャピン記述子で次のサポートを提供することで、圧縮されていないデータをキャプチャできます。

-   対応する[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)の構造体で、キャプチャピンがサポートする DataRanges メンバーの形式を一覧表示します。これは、 [**ksk datar**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体の配列です。 KS\_\_DATARANGE ポインターを提供します。この構造体は、KSDATARANGE ポインターとしてキャストされます。

-   各[**ks\_datarange VIDEO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)構造体の**videoinfoheader**メンバーで、 [**ks\_videoinfoheader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)構造体を提供します。 各 KS\_VIDEOINFOHEADER には、 [**ks\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)が含まれています。

-   MPEG2 キャプチャのバイナリ形式を公開するには、 **biCompression**を D3DDDIFMT\_binarybuffer に、 **biheight**を1に、 **biheight**をバイナリバッファーのサイズと等しくなるように設定します。

Avstream のシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)の*キャプチャ .cpp*ファイルには、前の一覧の項目の例が含まれています。

 

 




