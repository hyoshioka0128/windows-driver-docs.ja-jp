---
title: VRAM に圧縮されていないデータのキャプチャ
description: VRAM に圧縮されていないデータのキャプチャ
ms.assetid: efec607d-3337-40a5-812c-57292f201d54
keywords:
- VRAM キャプチャ WDK AVStream、圧縮されていないデータ
- WDK VRAM による非圧縮データをキャプチャします。
- WDK VRAM キャプチャを書式設定します。
- pin VRAM WDK AVStream の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59ef846fe259895bc3a0c5ce0dff4a4ffe017fc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561095"
---
# <a name="capturing-uncompressed-data-to-vram"></a>VRAM に圧縮されていないデータのキャプチャ


VRAM が有効な AVStream ミニドライバーは、キャプチャ暗証番号 (pin) の記述子では、次のサポートを提供することで圧縮されていないデータをキャプチャできます。

-   対応する[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)構造体のキャプチャの暗証番号 (pin) をサポートする形式を一覧に、 **DataRanges** の配列のメンバー、[**KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。 KS へのポインターを提供\_DATARANGE\_KSDATARANGE へのポインターとしてキャスト、ビデオの構造体。

-   **VideoInfoHeader**のそれぞれに所属[ **KS\_DATARANGE\_ビデオ**](https://msdn.microsoft.com/library/windows/hardware/ff567628)構造体を提供する[ **KS\_VIDEOINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567700)構造体。 各 KS\_VIDEOINFOHEADER が含まれています、 [ **KS\_BITMAPINFOHEADER**](https://msdn.microsoft.com/library/windows/hardware/ff567305)します。

-   MPEG2 キャプチャのバイナリ形式を公開するには、次のように設定します**biCompression** D3DDDIFMT 等しく\_BINARYBUFFER、 **biHeight** 1 に等しいと**biWidth**と等しく、。バイナリのバッファーのサイズ。

*Capture.cpp*のファイル、 [AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)上記のリスト項目の例が含まれています。

 

 




