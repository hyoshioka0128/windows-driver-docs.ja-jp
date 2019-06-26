---
title: KS のデータ形式とデータ範囲
description: KS のデータ形式とデータ範囲
ms.assetid: 44b55a5a-ec58-4c1e-b780-e20829fe3edf
keywords:
- ストリーミング データ形式の WDK カーネル
- ストリーミング形式の WDK カーネル
- WDK のカーネルがストリームの範囲します。
- ストリーミング データ範囲の WDK カーネル
- KS データ形式の WDK カーネルのストリーミング
- KS データ範囲 WDK カーネル ストリーミング
- KSDATARANGE
- KSDATAFORMAT
- カーネルの WDK、データ範囲のストリーミング
- KS WDK、データの範囲
- カーネルの WDK、データ形式のストリーミング
- KS WDK、データ形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 298a08b7027ea3a9a53698390d7a1563a67a9c49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382519"
---
# <a name="ks-data-formats-and-data-ranges"></a>KS のデータ形式とデータ範囲





KS ピン指定データ形式し、範囲を使用して、 [ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)と[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体。 データの形式では、データ ストリーム、16 ビットのオーディオのサンプリング サイズなどの単一の属性を指定します。 データ範囲を指定します、複数の形式などのオーディオ サンプリング 16 ~ 24 ビットの範囲。

ミニドライバーが各 KSDATARANGE 構造体の配列を含む[ **KSPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)が提供する構造体。 Microsoft 提供の形式で列挙*ksmedia.h*します。

KSDATARANGE 構造が KSDATAFORMAT 構造体と同じメンバーただし、ミニドライバーは KSDATARANGE の主要な形式、サブフォーマット、および指定子のメンバーのワイルドカード値を指定できます。

ミニドライバーでは、これらの構造の拡張のバージョンを使用して、メディア固有の値を定義します。 オーディオおよびビデオのキャプチャのしくみについてを参照してください。[オーディオ データ形式とデータ範囲](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-data-formats-and-data-ranges)と[Stream の形式を選択する](selecting-a-stream-format.md)します。

クライアントは、クエリのフィルターをピン留めする指定されたファクトリでインスタンス化される pin のデータ形式のサポートを次のプロパティを使用します。

-   [**KSPROPERTY\_PIN\_DATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)します。 KS フィルターは、pin の pin ファクトリによってインスタンス化でサポートされているすべてのデータ範囲を報告します。 これには、ピン留めできるすべてのデータ形式が含まれます*これまで*をサポートします。

-   [**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)します。 KS フィルターは、ピンの現在のドライバーの内部状態を暗証番号 (pin) ファクトリによってインスタンス化でサポートされているすべてのデータ範囲を報告します。

-   [**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)します。 クライアントは、pin の pin ファクトリによってインスタンス化、特定のデータ形式をサポートする場合、クエリには、このプロパティを使用できます。

-   [**KSPROPERTY\_PIN\_DATAINTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)します。 クライアントは、このプロパティを使用して、さまざまなデータ形式を提供することができます。

現在のデータが書式設定や、を通じてデータ形式の変更を要求、ユーザー モードのクライアントで確認できます、暗証番号 (pin) がインスタンス化されると[KSPROPSETID\_接続](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-connection)プロパティ要求。 たとえば、クライアントを使用して[ **KSPROPERTY\_接続\_PROPOSEDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-proposedataformat) pin が特定のデータ形式をサポートしているかを判断します。 クライアントを使用して[ **KSPROPERTY\_接続\_DATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-dataformat)データ形式を変更します。

KS ミニドライバーとクライアントでは、データ形式に動的にネゴシエートできます。 ストリームのデータ形式が変更されたときに、ミニドライバーは、KSSTREAM を指定\_ヘッダー\_OPTIONSF\_DATADISCONTINUITY フラグ、 **OptionsFlags** 、KSSTREAM のメンバー\_ヘッダー。 ミニドライバーは、新しいデータ自体で説明する形式を渡します、 [ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)対応するデータ バッファー内の構造体。

 

 




