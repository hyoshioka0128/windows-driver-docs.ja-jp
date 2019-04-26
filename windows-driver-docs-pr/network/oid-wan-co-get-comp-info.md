---
title: OID_WAN_CO_GET_COMP_INFO
description: OID_WAN_CO_GET_COMP_INFO OID 要求の NIC、またはそのドライバーの機能に関する情報を返すミニポート ドライバー具体的には、圧縮をサポートするかどうか。
ms.assetid: a2525548-ca5a-47a8-ab19-e0469913f6be
ms.date: 08/08/2017
keywords: -OID_WAN_CO_GET_COMP_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e0af4684bfedf1be715ee6fa599dcaa74cc7b8df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342322"
---
# <a name="oidwancogetcompinfo"></a>OID\_WAN\_CO\_取得\_COMP\_情報


OID\_WAN\_CO\_取得\_COMP\_情報 OID 要求の NIC、またはそのドライバーの機能に関する情報を返すミニポート ドライバー具体的には、圧縮をサポートするかどうか. そうである場合、返される値は、Point-to-Point プロトコル (PPP) 圧縮制御プロトコルでの圧縮をネゴシエートに使用されます。 プロトコルは、その後に PPP 圧縮スキームをネゴシエートし、 [OID\_WAN\_CO\_設定\_COMP\_情報](oid-wan-co-set-comp-info.md)要求。 この圧縮情報は、仮想の接続 (VC) に固有です。

圧縮情報は、NDIS\_WAN\_CO\_取得\_COMP\_情報構造体の次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_COMP_INFO {
         OUT NDIS_WAN_COMPRESS_INFO SendCapabilities;
         OUT NDIS_WAN_COMPRESS_INFO RecvCapabilities;
    } NDIS_WAN_CO_GET_COMP_INFO,   *PNDIS_WAN_CO_GET_COMP_INFO;
```




この構造体のメンバーには、次の情報が含まれます。

<a href="" id="sendcapabilities"></a>**SendCapabilities**  
データを送信するための圧縮機能に関する情報を含む構造体を指定します。

<a href="" id="recvcapabilities"></a>**RecvCapabilities**  
受信側のデータの圧縮機能に関する情報を含む構造体を指定します。

<a name="remarks"></a>注釈
-------

詳しくは、NDIS の\_WAN\_圧縮\_情報構造体を参照してください[OID\_WAN\_取得\_COMP\_情報](https://msdn.microsoft.com/library/windows/hardware/ff561202)します。

<a name="requirements"></a>要件
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


[OID\_WAN\_GET\_COMP\_INFO](https://msdn.microsoft.com/library/windows/hardware/ff561202)

[OID\_WAN\_CO\_SET\_COMP\_INFO](oid-wan-co-set-comp-info.md)








