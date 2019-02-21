---
title: データ範囲のプロパティ
description: データ範囲のプロパティ
ms.assetid: 84bdd151-a034-445e-9f6d-19940e32b2c1
keywords:
- 交差部分のデータ ハンドラーの WDK オーディオ、データ範囲プロパティ
- データの範囲は WDK オーディオ、プロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27c0abfe3f5cb5a2cc5c7bbb6b0653fe110e961e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532240"
---
# <a name="data-range-properties"></a>データ範囲のプロパティ


## <span id="data_range_properties"></span><span id="DATA_RANGE_PROPERTIES"></span>


データ範囲は、データの積集合のだけでなく使用されますが、デバイスのプロパティとしてアクセスできます (を参照してください[暗証番号 (pin) のデータ範囲は、プロパティの積集合](pin-data-range-and-intersection-properties.md))。 このため、そのピンをすべて形式ネゴシエーションの処理の交差部分のデータ ハンドラーのアダプター ドライバーは引き続きデータ範囲の完全なセットを含める必要があります。 データ範囲は、アダプターの交差部分のデータ ハンドラーが組み込まれたデータ形式の基本設定可能な限り密接に反映されます。

Pin のデータの範囲は、以下のプロパティを通じてアクセスできます。

[**KSPROPERTY\_PIN\_DATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565199)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565195)

これら 2 つのプロパティは、暗証番号 (pin) の静的データの範囲と制約されたデータ範囲をそれぞれ指定します。

制約されたデータ範囲は、他の目的で既に割り当てられている内蔵型のリソースのアカウントに動的に更新されるため、デバイスの現在の機能についてより正確な情報を提供します。 比較すると、静的なデータ範囲可能性があります正確に報告使用されなくなったリソースに依存しているハードウェア機能。

現在の PortCls 実装では、ポートのドライバーの既定の交差部分のデータ ハンドラーは、アダプターの静的なデータ範囲のみを使用します。

 

 




