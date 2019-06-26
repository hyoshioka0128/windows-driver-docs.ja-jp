---
title: OID_GEN_MAXIMUM_SEND_PACKETS
description: クエリとして OID_GEN_MAXIMUM_SEND_PACKETS OID には、ミニポート ドライバーの MiniportSendPackets 関数が受け入れることができる送信パケットの記述子の最大数を指定します。
ms.assetid: 7e87285f-26c5-4b7d-99a8-bc0f30c643dc
ms.date: 08/08/2017
keywords: -OID_GEN_MAXIMUM_SEND_PACKETS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 28ebd8a34c5347f0884c66c14d3764781913b573
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369053"
---
# <a name="oidgenmaximumsendpackets"></a>OID\_GEN\_最大\_送信\_パケット


クエリ、OID として\_GEN\_最大\_送信\_パケットの OID はの最大数の送信パケットの記述子を指定します、ミニポート ドライバーの[ *MiniportSendPackets*](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550524(v=vs.85))関数が受け入れることができます。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
使われていません。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
使われていません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

OID のクエリに対する応答の逆シリアル化されたドライバーによって返される値を無視する NDIS\_GEN\_最大\_送信\_パケット。 NDIS が逆シリアル化されたミニポート ドライバーの提供パケット記述子の配列のサイズを調整できません*MiniportSendPackets*関数。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportSendPackets*](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550524(v=vs.85))

 

 




