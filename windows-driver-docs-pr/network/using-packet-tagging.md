---
title: パケット タグ付けの使用
description: パケット タグ付けの使用
ms.assetid: a151256b-d69f-4abb-bf68-644f157dfdd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe6218d4bb52bb21a042c5a4162035482346af26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842979"
---
# <a name="using-packet-tagging"></a>パケット タグ付けの使用


コールアウトドライバーは、関心のあるパケットにタグを付け、タグ付けされたパケットに発生するイベントの通知を受け取ることができます。 パケットタグ付けは、windows 7 以降のバージョンの Windows でサポートされています。

パケットタグ付けを使用するには、コールアウトドライバーは[*fwps\_net\_buffer\_list*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)を実装する必要があります\_通知\_FN0 または[*FWPS\_net\_buffer\_LIST*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)\_\_FN1 callback に通知プロシージャ. この関数は、タグ付けされたパケットのすべての状態通知を受け取ります。 個々のパケットにタグを付けるには、 [**FwpsNetBufferListGetTagForContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)を呼び出して、コールアウトドライバーが特別なコンテキストタグを取得する必要があります。 コールアウトドライバーは、タグ付けされたパケットの一部またはすべてに対して同じコンテキストタグを使用できます。 たとえば、コールアウトドライバーは、異なるコンテキストタグを使用して、タグ付けされたパケットの種類を区別する場合があります。

パケットにタグを付けるために、コールアウトドライバーは[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を使用します。 コールアウトドライバーは、 [**FwpsNetBufferListAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)を呼び出して個々の**NET\_BUFFER\_LIST**構造体にタグを付けます。 コールアウトドライバーによってパケットに関連付けられるコンテキストは、任意の符号なし64ビット値です。 イベントがトリガーされると、 [*fwps\_net\_buffer\_list\_notify\_FN0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)または[*FWPS\_net\_buffer\_list\_通知\_FN1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1) callback は、コンテキストをとして渡します。入力パラメーター。コールアウトドライバーが個別のタグ付きパケットを識別できるようにします。 コンテキストは、フィルター処理エンジンによって使用または評価されません。 コールバックに渡されるのは、コールアウトドライバーによって使用される場合だけです。

パケットがスタックを離れると、コンテキストはタグ付きパケットから自動的に削除されます。 ただし、パケットが TCP/IP スタックに入力されない場合 (たとえば、NDIS フィルタードライバーの場合)、 *netBufferList*パラメーターを**NULL**に設定して[**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)を呼び出すことによって、コンテキストを手動で削除する必要があります。

コールアウトでタグ付け操作を早期に中止する必要がある場合は、 [**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)を呼び出すことによってコンテキストを削除できます。 コンテキストを削除すると、通常は**Fwps\_NET\_BUFFER\_LIST\_context\_削除さ**れたイベントがトリガーされます。 トリガーできるイベントの詳細については、 [**Fwps\_NET\_BUFFER\_LIST\_EVENT\_TYPE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)列挙体を参照してください。 場合によっては、パケットが処理のために TCP/IP スタックに入っていないなど、イベントがトリガーされないことがあります。

タグ付けされたパケットが複製されると、コールアウトドライバーは、そのコンテキストを複製パケットに移動またはコピーできます。 コンテキストを移動するには (複製の場合)、コールアウトドライバーは*Removecontext*パラメーターを**TRUE**に設定して[**FwpsNetBufferListRetrieveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)を呼び出す必要があります。 その後、コンテキストを新しいパケットに関連付けることができます。 コンテキストをコピーするプロセス (重複の場合) は、 **FwpsNetBufferListRetrieveContext0**の*Removecontext*パラメーターを**FALSE**に設定する必要がある点を除いて同じです。

TCP/IP レイヤーからタグ付けされたパケットは、 [NDIS フィルタードライバー](ndis-filter-drivers2.md)から取得できます。 この逆も当てはまります。 パケットタグ付けは、データセグメントを除くパケットが指定されていないストリームレイヤーからは使用できません。

コールアウトドライバは、 [*fwps\_net\_buffer\_リスト*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)の外部にあるパケットのコンテキストを取得し\_\_FN0 または[*FWPS\_net\_buffer\_list\_通知\_通知*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1) [**FwpsNetBufferListRetrieveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)を呼び出して関数を FN1 します。 通常、コールアウトドライバーは、その[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)によってコンテキストを取得します。

## <a name="related-topics"></a>関連トピック


[Classid (場合)](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[**FWPS\_NET\_BUFFER\_LIST\_イベント\_TYPE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)

[*FWPS\_NET\_BUFFER\_LIST\_通知\_FN0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)

[*FWPS\_NET\_BUFFER\_LIST\_通知\_FN1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)

[**FwpsNetBufferListAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)

[**FwpsNetBufferListGetTagForContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)

[**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)

[**FwpsNetBufferListRetrieveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[NDIS フィルタードライバー](ndis-filter-drivers2.md)

 

 






