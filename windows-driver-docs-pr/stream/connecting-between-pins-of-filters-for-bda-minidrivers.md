---
title: BDA ミニドライバー用フィルターのピン間接続
description: BDA ミニドライバー用フィルターのピン間接続
ms.assetid: 549031f3-1501-43c0-b172-bc88613d7e61
keywords:
- ドライバーのアーキテクチャの WDK AVStream、暗証番号 (pin) のデータ範囲のブロードキャストします。
- BDA WDK AVStream、データの範囲をピン留めします。
- データの範囲は WDK AVStream
- WDK AVStream を範囲します。
- 暗証番号 (pin) のデータ範囲 WDK
- 接続 WDK BDA をピン留め
- WDK BDA のピンを接続します。
- WDK BDA の接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e35c6ab3cd37933b211526363154c9dcbd544c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374190"
---
# <a name="connecting-between-pins-of-filters-for-bda-minidrivers"></a>BDA ミニドライバー用フィルターのピン間接続





BDA フィルターのピンが相互に接続できるように、これらのフィルターの BDA ミニドライバーする必要がありますが提供されますデータ範囲のピンの」の説明に従って[AVStream のデータ範囲の交差部分](data-range-intersections-in-avstream.md)します。 つまり、フィルターのピンは、これらのデータ範囲をサポートするその他のフィルターのピンにストリームに接続を有効にするサポートされるデータの範囲を指定します。

たとえば、BDA のピンをできるようにするチューナーとキャプチャ フィルター接続、チューナーのフィルターの出力ピンおよびキャプチャ フィルターの入力ピンは、次のデータ形式で設定が必要、 [ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)ピンの構造:

-   **MajorFormat**静的に設定\_KSDATAFORMAT\_型\_ストリーム

-   **サブフォーマット**静的に設定\_KSDATAFORMAT\_型\_MPEG2\_トランスポート

-   **指定子**静的に設定\_KSDATAFORMAT\_指定子\_BDA\_トランスポート

BDA のピンをできるようにするフィルターのキャプチャと demultiplex 接続、キャプチャ フィルターの出力ピンおよび demultiplex フィルターの入力ピンは、次のデータ形式で設定が必要、 [ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)ピンの構造:

-   **MajorFormat**静的に設定\_KSDATAFORMAT\_型\_ストリーム

-   **サブフォーマット**静的に設定\_KSDATAFORMAT\_サブタイプ\_BDA\_MPEG2\_トランスポート

-   **指定子**静的に設定\_KSDATAFORMAT\_指定子\_NONE

**注**   demultiplex フィルターの入力ピン、静的にしか設定\_KSDATAFORMAT\_サブタイプ\_BDA\_MPEG2\_トランスポート subformat 場合、AVStreamフィルターのミニドライバーは、準拠 BDA です。
入力ピンが静的に設定されている場合は、メディアの種類\_KSDATAFORMAT\_サブタイプ\_BDA\_MPEG2\_トランスポートとフィルター BDA 規則に準拠していない、放送信号が正しくレンダリングされない可能性があります。

 

 

 




