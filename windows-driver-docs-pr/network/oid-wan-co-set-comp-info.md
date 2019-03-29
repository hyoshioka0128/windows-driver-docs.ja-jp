---
title: OID_WAN_CO_SET_COMP_INFO
description: OID_WAN_CO_SET_COMP_INFO OID には、PPP 圧縮スキームをミニポート ドライバー既に返される情報を OID_WAN_CO_GET_COMP_INFO クエリでプロトコルが選択したのミニポート ドライバーに通知します。
ms.assetid: f3b6b846-fa8c-425b-ba05-45927e744d66
ms.date: 08/08/2017
keywords: -OID_WAN_CO_SET_COMP_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 574d3fcc2015278bd6fb41a9e9086fde02af3d30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577929"
---
# <a name="oidwancosetcompinfo"></a>OID\_WAN\_CO\_設定\_COMP\_情報


OID\_WAN\_CO\_設定\_COMP\_情報 OID に通知するミニポート ドライバー既に返される情報をでプロトコルが選択したPPPcompressionschemeのミニポートドライバー[OID\_WAN\_CO\_取得\_COMP\_情報](oid-wan-co-get-comp-info.md)クエリ。 この PPP 圧縮スキームは、仮想の接続 (VC) に固有です。

プロトコル、NDIS で選択されていること、PPP compression scheme の仕様を提供する\_WAN\_CO\_設定\_COMP\_情報構造体の次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_SET_COMP_INFO {
         IN NDIS_WAN_COMPRESS_INFO SendCapabilities;
         IN NDIS_WAN_COMPRESS_INFO RecvCapabilities;
    } NDIS_WAN_CO_SET_COMP_INFO,   *PNDIS_WAN_CO_SET_COMP_INFO;
```




この構造体のメンバーには、次の情報が含まれます。

<a href="" id="sendcapabilities"></a>**SendCapabilities**  
データを送信するための圧縮機能に関する情報を含む構造体を指定します。

<a href="" id="recvcapabilities"></a>**RecvCapabilities**  
受信側のデータの圧縮機能に関する情報を含む構造体を指定します。

<a name="remarks"></a>コメント
-------

詳しくは、NDIS の\_WAN\_圧縮\_情報構造体を参照してください[OID\_WAN\_取得\_COMP\_情報](https://msdn.microsoft.com/library/windows/hardware/ff561202)します。

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


[OID\_WAN\_CO\_GET\_COMP\_INFO](oid-wan-co-get-comp-info.md)








