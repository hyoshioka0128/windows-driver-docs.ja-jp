---
title: リトリート操作
description: リトリート操作
ms.assetid: fdf1228b-ccae-4079-b968-b4dbb5665555
keywords:
- ネットワークデータ WDK、retreat 操作
- データ WDK ネットワーク、retreat 操作
- パケット WDK ネットワーク、retreat 操作
- retreat 操作 (WDK ネットワーク)
- データの送信 (WDK ネットワーク)
- データを受信する WDK ネットワーク
- MDLs の割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5036adad93426679002c27cc76509181828580bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842015"
---
# <a name="retreat-operations"></a>リトリート操作





Retreat 操作は、net [ **\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造、または[**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造内のすべての net\_バッファー構造で使用されているデータ領域のサイズを増やすことができます。

NDIS には、次のような retreat 関数が用意されています。

[**NdisRetreatNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart)

[**NdisRetreatNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferlistdatastart)

Retreat 操作は、NET\_のバッファー構造に関連付けられている MDLs を割り当てることがあります。 MDLs を割り当てるメカニズムを提供するために、ドライバーは[**NetAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_allocate_mdl_handler)関数の省略可能なエントリポイントを提供できます。 エントリポイントが**NULL**の場合、NDIS は既定のメソッドを使用して mdls を割り当てます。 MDLs は、MDL を割り当てるために使用されたメカニズムの逆数を提供する[**Netfreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-net_buffer_free_mdl_handler)関数内で解放する必要があります。

新しい**datalength**を取得するために、NDIS はドライバーによって指定された*DataOffsetDelta*を現在の**datalength**に追加します。 使用されていない*データ領域*のサイズが*DataOffsetDelta*より大きい場合は、retreat 操作によって**DataOffset**が減少します。 この場合、新しい**DataOffset**は、現在の**DataOffset**から*DataOffsetDelta*を引いたものになります。

*DataOffsetDelta*が**DataOffset**より大きい場合は、retreat 操作によって新しいデータ領域が割り当てられます。 この場合、NDIS はそれに応じて**DataOffset**を調整します。

送信操作の場合、解放要求を満たすのに十分な*未使用データ領域*がない場合、NDIS はメモリを割り当てます。 メモリ割り当てが不要な場合、NDIS は単に**DataOffset**と**DataLength**を調整します。 パフォーマンスを向上させるために、ドライバーは、すべての基になるドライバーの retreat 操作に対応するために、送信前に十分なデータサイズを割り当てておく必要があります。

Receive return の場合、NDIS はそれに応じて**DataOffset**と**DataLength**を調整します。 Retreat 操作は、受信処理中に発生した詳細な操作を元に戻します。 Retreat 操作の後、*使用されたデータ領域*には、受信処理中に使用された、基になるドライバーのヘッダーデータが格納されます。

 

 





