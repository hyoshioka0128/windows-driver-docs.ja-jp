---
title: リトリート操作
description: リトリート操作
ms.assetid: fdf1228b-ccae-4079-b968-b4dbb5665555
keywords:
- ネットワーク データ WDK、撤退操作
- データの WDK ネットワー キング、撤退操作
- パケット WDK ネットワー キング、撤退操作
- 撤退操作 WDK ネットワーク
- WDK ネットワークのデータを送信します。
- 受信側のデータの WDK ネットワーク
- MDLs の割り当てください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c627ac99fb778ce7a3346f899804f5ce77c9b306
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362933"
---
# <a name="retreat-operations"></a>リトリート操作





撤退操作で使用されるデータ領域のサイズを増やすことができます、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体またはすべての NET\_内バッファーの構造体、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

NDIS には、次の撤退関数が用意されています。

[**NdisRetreatNetBufferDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564527)

[**NdisRetreatNetBufferListDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564529)

撤退操作では、NET に関連付けられている MDLs を割り当てることができる場合があります\_バッファーの構造体。 ドライバー MDLs を割り当てるための機能を提供するための省略可能なエントリ ポイントを提供できます、 [ **NetAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff568326)関数。 エントリ ポイントがある場合**NULL**NDIS では、既定のメソッドを使用して、MDLs を割り当てます。 内で MDLs を解放する必要があります、 [ **NetFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff568348) MDL の割り当てに使用されたメカニズムの逆数を提供する関数。

新しいを取得する**DataLength**、NDIS ドライバー指定を追加します*DataOffsetDelta*現在**DataLength**します。 場合のサイズ、*未使用データ領域*がより大きい、 *DataOffsetDelta*、撤退操作の軽減、 **DataOffset**します。 この場合、新しい**DataOffset**は現在**DataOffset**マイナス、 *DataOffsetDelta*します。

場合、 *DataOffsetDelta*がより大きい**DataOffset**、撤退操作は、新しいデータ領域を割り当てます。 この場合は、NDIS の調整、 **DataOffset**それに応じて。

NDIS がない場合に十分なメモリを割り当てます、送信操作の*未使用データ領域*撤退要求を満たすため。 NDIS を単純に調整メモリの割り当てが必要ない場合、 **DataOffset**と**DataLength**します。 パフォーマンスの向上のため、ドライバーは、すべての基になるドライバーの撤退操作に対応するために送信する前に十分なデータの合計サイズを割り当てる必要があります。

NDIS 受信戻り値の場合、調整だけ、 **DataOffset**と**DataLength**それに応じて。 した高度な操作が配置中に撤退操作の逆の処理が表示されます。 撤退操作後に、*使用データ領域*中に使用される基になるドライバーが処理を受信するヘッダー データが含まれています。

 

 





