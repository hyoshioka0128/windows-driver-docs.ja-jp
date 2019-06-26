---
title: OID_GEN_MACHINE_NAME
description: セットとして OID_GEN_MACHINE_NAME OID はミニポート ドライバーをローカル コンピューターの名前を示します。
ms.assetid: 771d21ff-e989-4717-8f3e-28f4b8afe274
ms.date: 08/08/2017
keywords: -OID_GEN_MACHINE_NAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bd5874b3ad7e02d0953b7ab2b86bd68cb46d0ea8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369067"
---
# <a name="oidgenmachinename"></a>OID\_GEN\_マシン\_名


OID、セットとして\_GEN\_マシン\_名の OID がミニポート ドライバーをローカル コンピューター名を示します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a name="remarks"></a>注釈
-------

この要求で渡された情報バッファーには、ローカル コンピューターの名前を表す Unicode 文字の配列が含まれています。 **InformationBufferLength**に用意されている値、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数をこの配列の長さを指定します (バイト単位)、NULL は含まないターミネータ。

NDIS 設定 OID\_GEN\_マシン\_ミニポート ドライバーが初期化が完了した後に名前を 1 回だけです。 Windows XP で NDIS 動的に通知が送信されません、コンピューター名の変更のミニポート ドライバー。 コンピューター名を変更した後、ユーザーは NDIS ミニポート ドライバーの新しいコンピューター名を通知するようにコンピューターを再起動する必要があります。

<a name="requirements"></a>必要条件
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


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)

 

 




