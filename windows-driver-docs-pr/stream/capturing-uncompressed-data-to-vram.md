---
title: 圧縮されていないデータの VRAM へのキャプチャ
description: 圧縮されていないデータの VRAM へのキャプチャ
ms.assetid: efec607d-3337-40a5-812c-57292f201d54
keywords:
- VRAM キャプチャ WDK AVStream、圧縮されていないデータ
- WDK VRAM による非圧縮データをキャプチャします。
- WDK VRAM キャプチャを書式設定します。
- pin VRAM WDK AVStream の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2591c90b824ef820933c212b71c88761b4a86c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386663"
---
# <a name="capturing-uncompressed-data-to-vram"></a>圧縮されていないデータの VRAM へのキャプチャ


VRAM が有効な AVStream ミニドライバーは、キャプチャ暗証番号 (pin) の記述子では、次のサポートを提供することで圧縮されていないデータをキャプチャできます。

-   対応する[ **KSPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)構造体のキャプチャの暗証番号 (pin) をサポートする形式を一覧に、 **DataRanges** の配列のメンバー、[**KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体。 KS へのポインターを提供\_DATARANGE\_KSDATARANGE へのポインターとしてキャスト、ビデオの構造体。

-   **VideoInfoHeader**のそれぞれに所属[ **KS\_DATARANGE\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video)構造体を提供する[ **KS\_VIDEOINFOHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_videoinfoheader)構造体。 各 KS\_VIDEOINFOHEADER が含まれています、 [ **KS\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)します。

-   MPEG2 キャプチャのバイナリ形式を公開するには、次のように設定します**biCompression** D3DDDIFMT 等しく\_BINARYBUFFER、 **biHeight** 1 に等しいと**biWidth**と等しく、。バイナリのバッファーのサイズ。

*Capture.cpp*のファイル、 [AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)上記のリスト項目の例が含まれています。

 

 




