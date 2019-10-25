---
title: パケット表示形式
description: パケット表示形式
ms.assetid: 37ee6db6-2f0e-4987-85e9-5362d23d7b27
keywords:
- パケット表示 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d060b728cab3c98eff66f6ab4a5f2fe5e2a8fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843713"
---
# <a name="packet-indication-format"></a>パケット表示形式


ネットワークデータは、WFP で NDIS net buffer リスト ([**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)) として示されています。 **Net\_buffer\_LIST**構造体の**次**のメンバーは、一連の net BUFFER*リストを記述*するために使用できます。 WFP は、次の場合を除き、コールアウトに対して1つのネットバッファーリスト (つまり、netBufferList&gt;の次の = = **NULL**) を示します。

-   WFP は、ストリームレイヤーからのコールアウトへのネットワークバッファーリストチェーンを示すことができます。

-   WFP は、コールアウトへの転送パスに IP パケットフラグメントグループを分類するときに、ネットワークバッファーリストチェーンをコールアウトに示します。 チェーン内の各 net buffer list は、1つのフラグメントを記述します。

ネットワークバッファーの一覧はパケット全体を表すことができますが、さまざまな種類のレイヤーの場合、WFP は、IP ヘッダーの先頭とは異なるオフセットでコールアウトされるように、net buffer リストを示します。 たとえば、受信ネットワークレイヤーでは、IP ヘッダーの後に net バッファーリストが開始され、受信トランスポート層では、トランスポートヘッダーの後に net buffer リストが開始されます。 IP ヘッダーとトランスポートヘッダーは常に、net バッファーリスト内の最初の[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造によって記述されます。

Net buffer リストへのオフセットは、 [**Fwps\_受信\_メタデータ\_VALUES0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)構造体の**ipheadersize**メンバーと**transportHeaderSize**メンバーを使用して、コールアウトに示されます。 コールアウトは、NDIS 関数[**NdisRetreatNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart)と[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart)を使用して、指定されたネットワークバッファー一覧のオフセットを調整できます。 ただし、この場合、コールアウトは、 [*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)の年関数から戻る前にオフセットの調整を元に戻す必要があります。

送信データに対する*classid*の年関数の呼び出しでは、 [**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)に複数の[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体を含めることができます。それぞれが IP パケットを表します。 Net バッファーの一覧にある一部のパケット (たとえば、net buffer) が許容されていても、その他のパケットがない場合、コールアウトドライバーは次の操作を行う必要があります。

1.  Net バッファーリスト全体を複製してブロックします。

2.  ネットワークバッファーの許容されるサブセットを記述する新しい net buffer リストを作成します。

3.  新しい net buffer リストを送信パスに再び挿入します。

また、コールアウトは、net buffer リストから不要なネットワークバッファーのリンクを解除し、変更されたネットワークバッファーリストを送信パスに再び挿入することもできます。 ただし、この場合、コールアウトドライバーは、 [**FwpsFreeCloneNetBufferList0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)関数を呼び出す前に、複製された net バッファーの一覧に対してこの変更を元に戻す必要があります。 また、コールアウトドライバーは、元の net buffer リンケージ情報を状態データの一部として保存する必要があります。

WFP で使用されるデータオフセットの詳細については、「[データオフセット位置](https://docs.microsoft.com/windows-hardware/drivers/network/data-offset-positions)」を参照してください。

**注**  、暗号化を解除された IPSec ESP パケットで動作するコールアウトは、パケット長を決定するために、MDL データではなく、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造のデータ長を使用する必要があります。 データ長を取得するには、 [**NET\_BUFFER\_data\_length**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-data-length)マクロを使用します。 詳細については、「 [IPsec と互換性のあるコールアウトドライバーの開発](developing-ipsec-compatible-callout-drivers.md)」を参照してください。

 

 

 





