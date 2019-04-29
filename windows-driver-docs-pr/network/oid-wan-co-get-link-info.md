---
title: OID_WAN_CO_GET_LINK_INFO
description: OID_WAN_CO_GET_LINK_INFO OID は、PPP フレーム (VC) の仮想接続の現在の状態情報を返します、ミニポート ドライバーを要求します。 この情報は、次のように定義されている NDIS_WAN_CO_GET_LINK_INFO 構造体で返されます。
ms.assetid: 26582bc4-c32f-4243-a208-9230c62f4d16
ms.date: 08/08/2017
keywords: -OID_WAN_CO_GET_LINK_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9700321d6e839163462b7b06d9dacc00be4f23df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390663"
---
# <a name="oidwancogetlinkinfo"></a>OID\_WAN\_CO\_取得\_リンク\_情報


OID\_WAN\_CO\_取得\_リンク\_OID の情報は、PPP フレーム (VC) の仮想接続の現在の状態情報を返します、ミニポート ドライバーを要求します。 この情報は、NDIS\_WAN\_CO\_取得\_リンク\_情報構造体の次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_LINK_INFO {
         OUT ULONG MaxSendFrameSize;
         OUT ULONG MaxRecvFrameSize;
         OUT ULONG SendFramingBits;
         OUT ULONG RecvFramingBits;
         OUT ULONG SendCompressionBits;
         OUT ULONG RecvCompressionBits;
         OUT ULONG SendACCM;
         OUT ULONG RecvACCM;
    } NDIS_WAN_CO_GET_LINK_INFO,   *PNDIS_WAN_CO_GET_LINK_INFO;
```




この構造体のメンバーには、次の情報が含まれます。

<a href="" id="maxsendframesize"></a>**MaxSendFrameSize**  
ミニポート ドライバーは、この VC での送信に受け入れることができるをバイト単位で最大バッファー サイズを指定します。 ミニポート ドライバーの*MiniportCoSendPackets*関数がこのサイズよりも大きい着信、送信パケットを拒否します。

<a href="" id="maxrecvframesize"></a>**MaxRecvFrameSize**  
ネットワークから受信する最大のパケットを指定します。 ミニポート ドライバーでは、大規模なパケットを削除できます。

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
非同期のメディアの種類、論理ビット 0 ~ 31 溜まってバイトをそれぞれバイトを指定します。 つまり、ビット 0 が 1 に設定されている場合、ASCII 文字 0x00 する必要がありますバイトで配置してなど。

<a href="" id="recvaccm"></a>**RecvACCM**  
説明に従って**SendACCM**します。

<a name="remarks"></a>注釈
-------

指定できる値**SendFramingBits**と**RecvFramingBits** OID への応答で返されるドライバーが含まれて\_WAN\_CO\_取得\_リンク\_INFO であるクエリ。

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


[OID\_WAN\_CO\_取得\_リンク\_情報](oid-wan-co-get-link-info.md)








