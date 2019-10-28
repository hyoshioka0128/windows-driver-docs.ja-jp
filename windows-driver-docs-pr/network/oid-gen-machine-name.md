---
title: OID_GEN_MACHINE_NAME
description: セットとして、OID_GEN_MACHINE_NAME OID はミニポートドライバーへのローカルコンピューター名を示します。
ms.assetid: 771d21ff-e989-4717-8f3e-28f4b8afe274
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_MACHINE_NAME ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 74d92e7df9a4d41bb4cd95620a4084a34c034638
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843069"
---
# <a name="oid_gen_machine_name"></a>OID\_GEN\_マシン\_名


設定として、OID\_GEN\_マシン\_名前 OID は、ミニポートドライバーへのローカルコンピューター名を示します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

この要求で渡される情報バッファーには、ローカルコンピューター名を表す Unicode 文字の配列が含まれています。 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数に指定された**informationbufferlength**値は、この配列の長さをバイト単位で指定します。 NULL 終端文字は含まれません。

ミニポートドライバーの初期化が完了した後に1回だけ、NDIS は OID\_\_\_GEN に設定します。 Windows XP では、NDIS はコンピューター名の変更をミニポートドライバーに動的に通知しません。 コンピューター名を変更した後、NDIS がミニポートドライバーに新しいコンピューター名を通知するように、ユーザーはコンピューターを再起動する必要があります。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

 

 




