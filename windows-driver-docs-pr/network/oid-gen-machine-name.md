---
title: OID_GEN_MACHINE_NAME
description: セットとして OID_GEN_MACHINE_NAME OID はミニポート ドライバーをローカル コンピューターの名前を示します。
ms.assetid: 771d21ff-e989-4717-8f3e-28f4b8afe274
ms.date: 08/08/2017
keywords: -OID_GEN_MACHINE_NAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b08f79c86d00efd9930443c1ae8229b14ae7487f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538563"
---
# <a name="oidgenmachinename"></a>OID\_GEN\_マシン\_名


OID、セットとして\_GEN\_マシン\_名の OID がミニポート ドライバーをローカル コンピューター名を示します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

この要求で渡された情報バッファーには、ローカル コンピューターの名前を表す Unicode 文字の配列が含まれています。 **InformationBufferLength**に用意されている値、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数をこの配列の長さを指定します (バイト単位)、NULL は含まないターミネータ。

NDIS 設定 OID\_GEN\_マシン\_ミニポート ドライバーが初期化が完了した後に名前を 1 回だけです。 Windows XP で NDIS 動的に通知が送信されません、コンピューター名の変更のミニポート ドライバー。 コンピューター名を変更した後、ユーザーは NDIS ミニポート ドライバーの新しいコンピューター名を通知するようにコンピューターを再起動する必要があります。

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


[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

 

 




