---
title: 圧縮されていないデータの VRAM へのキャプチャ
description: 非圧縮データを VRAM にキャプチャする
ms.assetid: efec607d-3337-40a5-812c-57292f201d54
keywords:
- VRAM キャプチャ WDK AVStream、非圧縮データ
- 非圧縮データ WDK VRAM キャプチャ
- WDK VRAM キャプチャの形式
- 固定 VRAM 処理 WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 128cd3c4d05a1d8da1ca0205b8674dd17b7bd152
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812450"
---
# <a name="capturing-uncompressed-data-to-vram"></a>非圧縮データを VRAM にキャプチャする

VRAM が有効になっている AVStream ミニドライバーは、キャプチャピン記述子で次のサポートを提供することで、圧縮されていないデータをキャプチャできます。

- 対応する[**Kspin \_ 記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)の構造体で、キャプチャピンがサポートする**DataRanges**メンバーの形式を一覧表示します。これは、 [**ksdatarange**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体の配列です。 KS \_ \_ datarange ポインターとしてキャストする KS datarange ビデオ構造体へのポインターを提供します。

- 各[**ks \_ datarange \_ ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)構造の**videoinfoheader**メンバーで、 [**ks \_ videoinfoheader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)構造体を指定します。 各 KS \_ videoinfoheader には、 [**ks \_ bitmapinfoheader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)が含まれています。

- MPEG2 キャプチャのバイナリ形式を公開するには、 **biCompression**を D3DDDIFMT \_ Binarybuffer に、 **biheight**を1に、 **biheight**をバイナリバッファーのサイズと等しくなるように設定します。

Avstream のシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)の*キャプチャ .cpp*ファイルには、前の一覧の項目の例が含まれています。
