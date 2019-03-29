---
title: OID_WAN_CO_SET_LINK_INFO
description: OID_WAN_CO_SET_LINK_INFO OID は、特定の仮想接続 (VC) の PPP フレームの情報を設定するミニポート ドライバーを要求します。 プロトコルは、この PPP フレームの情報を示すために、次のように定義されている NDIS_WAN_CO_SET_LINK_INFO 構造体を使用します。
ms.assetid: 4487289a-01f6-4ae1-b660-3011d66acb29
ms.date: 08/08/2017
keywords: -OID_WAN_CO_SET_LINK_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0fada7f6db4ff5dc8e7ac56302de940f32a2fb1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579116"
---
# <a name="oidwancosetlinkinfo"></a>OID\_WAN\_CO\_設定\_リンク\_情報


OID\_WAN\_CO\_設定\_リンク\_OID の情報は、特定の仮想接続 (VC) の PPP フレームの情報を設定するミニポート ドライバーを要求します。 プロトコルは、NDIS\_WAN\_CO\_設定\_リンク\_情報構造体のこの PPP フレームの情報を示すために、次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_SET_LINK_INFO {
         IN ULONG MaxSendFrameSize;
         IN ULONG MaxRecvFrameSize;
         IN ULONG SendFramingBits;
         IN ULONG RecvFramingBits;
         IN ULONG SendCompressionBits;
         IN ULONG RecvCompressionBits;
         IN ULONG SendACCM;
         IN ULONG RecvACCM;
    } NDIS_WAN_CO_SET_LINK_INFO,   *PNDIS_WAN_CO_SET_LINK_INFO;
```




この構造体のメンバーには、次の情報が含まれます。

<a href="" id="maxsendframesize"></a>**MaxSendFrameSize**  
この VC のプロトコルが送信されます (バイト単位)、バッファーの最大値を指定します。 この値のミニポート ドライバーによって返された未満である必要があります、 [OID\_WAN\_CO\_取得\_リンク\_情報](oid-wan-co-get-link-info.md)クエリ。

ミニポート ドライバーの*MiniportCoSendPackets*関数は、このリンクの送信をこの値を超える送信パケットを拒否できます。

<a href="" id="maxrecvframesize"></a>**MaxRecvFrameSize**  
その後、プロトコルを受信する最大のネットワーク パケットを指定します。 この値は、OID のミニポート ドライバーによって返された未満である必要があります\_WAN\_CO\_取得\_リンク\_INFO であるクエリ。 ミニポート ドライバーでは、この大きい VC の任意の受信パケットを削除できます。

<a href="" id="sendframingbits"></a>**SendFramingBits**  
送信されるフレームの種類を示す送信フレーム ビットを指定します。 ミニポート ドライバーとの間の非互換性を検出した場合**SendFramingBits**と**RecvFramingBits**、NDIS 返します\_状態\_無効な\_データ。

可能な場合は、フレームの bits に基づいて、適切な NLPID とフレーム形式を使用する必要があります。

<a href="" id="recvframingbits"></a>**RecvFramingBits**  
受信されるフレームの種類を示す受信フレーム ビットを指定します。

<a href="" id="sendcompressionbits"></a>**SendCompressionBits**  
予約済み。

<a href="" id="recvcompressionbits"></a>**RecvCompressionBits**  
予約済み。

<a href="" id="sendaccm"></a>**SendACCM**  
非同期のメディアの種類、論理ビット 0 ~ 31 溜まってバイトをそれぞれバイトを指定します。 つまり、ビット 0 がいずれかに設定されている場合、ASCII 文字 0x00 する必要がありますバイトで配置してなど。

<a href="" id="recvaccm"></a>**RecvACCM**  
説明に従って**SendACCM**します。

<a name="remarks"></a>コメント
-------

指定できる値**SendFramingBits**と**RecvFramingBits**への応答で返される基になるドライバーが含まれて、 [OID\_WAN\_CO\_取得\_情報](oid-wan-co-get-info.md)クエリ。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WAN\_CO\_取得\_情報](oid-wan-co-get-info.md)

[OID\_WAN\_CO\_取得\_リンク\_情報](oid-wan-co-get-link-info.md)








