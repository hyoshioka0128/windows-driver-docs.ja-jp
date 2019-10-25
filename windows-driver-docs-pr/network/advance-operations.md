---
title: アドバンス操作
description: アドバンス操作
ms.assetid: 42554221-201d-4014-900d-435a47b3afa1
keywords:
- ネットワークデータ WDK, 事前操作
- データ WDK ネットワーク, 事前操作
- パケット WDK ネットワーク、事前操作
- 高度操作 WDK ネットワーク
- データの送信 (WDK ネットワーク)
- データを受信する WDK ネットワーク
- MDLs の解放
- 使用量の削減
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3dd93025b08dae8f6e8fd7a01431e7a8699c87b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838235"
---
# <a name="advance-operations"></a>アドバンス操作





Advance 操作は、net [ **\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造、または[**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造内のすべての net\_バッファー構造で使用されるデータ領域のサイズを縮小します。

ドライバーは、次のように高度に機能します。

[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart)

[**NdisAdvanceNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferlistdatastart)

詳細な操作では、NET\_のバッファー構造に関連付けられている MDLs が解放される場合があります。 MDLs を解放するためのメカニズムを提供するために、ドライバーは[**Netfreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_free_mdl_handler)関数の省略可能なエントリポイントを提供できます。 エントリポイントが**NULL**の場合、NDIS は既定のメソッドを使用して mdls を割り当てます。 MDLs は、 [**NetAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_allocate_mdl_handler)関数での MDL の割り当てに使用されたメカニズムの逆数を使用して、 *Netfreemdl*内でのみ解放する必要があります。

新しい**datalength**を取得するために、NDIS はドライバーによって指定された*DataOffsetDelta*を現在の**datalength**から減算します。 前の retreat 操作によって新しいデータ領域が割り当てられた場合、事前操作によって、以前に割り当てられたメモリが解放される可能性があります。 アドバンス操作でメモリが解放されない場合、NDIS は*DataOffsetDelta*を現在の**DataOffset**に追加して新しい**DataOffset**を取得します。 Advance 操作によってメモリが解放された場合、NDIS はそれに応じて**DataOffset**を調整します。

Send complete の場合は、前の retreat 操作で割り当てられたメモリを解放できます。 パフォーマンスを向上させるために、ドライバーは、すべての基になるドライバーの retreat 操作に対応するために、送信前に十分なデータサイズを割り当てておく必要があります。

受信を示す場合、アドバンス操作では、それに応じて**DataOffset**と**DataLength**を調整するだけです。 事前操作の後、下位層のヘッダーは*未使用のデータ領域*に残ります。

 

 





