---
title: アドバンス操作
description: アドバンス操作
ms.assetid: 42554221-201d-4014-900d-435a47b3afa1
keywords:
- ネットワーク データ WDK、高度な操作
- データの WDK ネットワーク、高度な操作
- パケットの WDK ネットワーク、高度な操作
- 高度な操作の WDK ネットワーク
- WDK ネットワークのデータを送信します。
- 受信側のデータの WDK ネットワーク
- MDLs の解放
- 使用回数を少なく
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09f1f6860c82c47bea272da920dc803d4d35e8cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574979"
---
# <a name="advance-operations"></a>アドバンス操作





高度な操作で使用されるデータ領域のサイズを小さく、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体またはすべての NET\_内バッファーの構造体、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

ドライバーは、次の高度な関数を使用します。

[**NdisAdvanceNetBufferDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff560703)

[**NdisAdvanceNetBufferListDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff560704)

高度な操作ことができます、NET に関連付けられている MDLs が解放される場合があります\_バッファーの構造体。 ドライバー MDLs を解放するための機構を提供するための省略可能なエントリ ポイントを提供できます、 [ **NetFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff568348)関数。 エントリ ポイントがある場合**NULL**NDIS では、既定のメソッドを使用して、MDLs を割り当てます。 MDLs は内でのみ解放する必要があります、 *NetFreeMdl*で MDL の割り当てに使用されたメカニズムの逆数を使用して、 [ **NetAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff568326)関数。

新しいを取得する**DataLength**、NDIS ドライバーが指定したを減算します*DataOffsetDelta*現在から**DataLength**します。 前の撤退操作に新しいデータ領域が割り当てられている場合、高度な操作は、このような以前に割り当てられたメモリを解放できます。 NDIS が単純に追加する高度な操作がメモリを確保できない場合、 *DataOffsetDelta*現在**DataOffset**新しいを取得する**DataOffset**します。 NDIS を調整します。 高度な操作は、メモリを解放する場合、 **DataOffset**それに応じて。

送信の完全なケースでは、高度な操作は前撤退操作で割り当てられたメモリを解放できます。 パフォーマンスの向上のため、ドライバーは、すべての基になるドライバーの撤退操作に対応するために送信する前に十分なデータの合計サイズを割り当てる必要があります。

受信を示す値の場合、高度な操作を単純に調整する、 **DataOffset**と**DataLength**それに応じて。 高度な操作後に下位層のヘッダーのままで、*未使用データ領域*します。

 

 





