---
title: KS データ形式とデータの範囲
description: KS データ形式とデータの範囲
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
ms.openlocfilehash: 3e62c95a50ff421fa10d9ce070096cb49b3d50df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530680"
---
# <a name="ks-data-formats-and-data-ranges"></a>KS データ形式とデータの範囲





KS ピン指定データ形式し、範囲を使用して、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)と[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。 データの形式では、データ ストリーム、16 ビットのオーディオのサンプリング サイズなどの単一の属性を指定します。 データ範囲を指定します、複数の形式などのオーディオ サンプリング 16 ~ 24 ビットの範囲。

ミニドライバーが各 KSDATARANGE 構造体の配列を含む[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)が提供する構造体。 Microsoft 提供の形式で列挙*ksmedia.h*します。

KSDATARANGE 構造が KSDATAFORMAT 構造体と同じメンバーただし、ミニドライバーは KSDATARANGE の主要な形式、サブフォーマット、および指定子のメンバーのワイルドカード値を指定できます。

ミニドライバーでは、これらの構造の拡張のバージョンを使用して、メディア固有の値を定義します。 オーディオおよびビデオのキャプチャのしくみについてを参照してください。[オーディオ データ形式とデータ範囲](https://msdn.microsoft.com/library/windows/hardware/ff536189)と[Stream の形式を選択する](selecting-a-stream-format.md)します。

クライアントは、クエリのフィルターをピン留めする指定されたファクトリでインスタンス化される pin のデータ形式のサポートを次のプロパティを使用します。

-   [**KSPROPERTY\_PIN\_DATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565199)します。 KS フィルターは、pin の pin ファクトリによってインスタンス化でサポートされているすべてのデータ範囲を報告します。 これには、ピン留めできるすべてのデータ形式が含まれます*これまで*をサポートします。

-   [**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565195)します。 KS フィルターは、ピンの現在のドライバーの内部状態を暗証番号 (pin) ファクトリによってインスタンス化でサポートされているすべてのデータ範囲を報告します。

-   [**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff565206)します。 クライアントは、pin の pin ファクトリによってインスタンス化、特定のデータ形式をサポートする場合、クエリには、このプロパティを使用できます。

-   [**KSPROPERTY\_PIN\_DATAINTERSECTION**](https://msdn.microsoft.com/library/windows/hardware/ff565198)します。 クライアントは、このプロパティを使用して、さまざまなデータ形式を提供することができます。

現在のデータが書式設定や、を通じてデータ形式の変更を要求、ユーザー モードのクライアントで確認できます、暗証番号 (pin) がインスタンス化されると[KSPROPSETID\_接続](https://msdn.microsoft.com/library/windows/hardware/ff566568)プロパティ要求。 たとえば、クライアントを使用して[ **KSPROPERTY\_接続\_PROPOSEDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff565107) pin が特定のデータ形式をサポートしているかを判断します。 クライアントを使用して[ **KSPROPERTY\_接続\_DATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff565103)データ形式を変更します。

KS ミニドライバーとクライアントでは、データ形式に動的にネゴシエートできます。 ストリームのデータ形式が変更されたときに、ミニドライバーは、KSSTREAM を指定\_ヘッダー\_OPTIONSF\_DATADISCONTINUITY フラグ、 **OptionsFlags** 、KSSTREAM のメンバー\_ヘッダー。 ミニドライバーは、新しいデータ自体で説明する形式を渡します、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)対応するデータ バッファー内の構造体。

 

 




