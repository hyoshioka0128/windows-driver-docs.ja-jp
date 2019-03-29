---
title: OID_GEN_SUPPORTED_LIST
description: クエリとして OID_GEN_SUPPORTED_LIST OID には、ミニポート ドライバーまたは NIC をサポートするオブジェクトの Oid の配列を指定します。
ms.assetid: 4e663204-eee0-4732-83c9-ec1dacd41034
ms.date: 08/08/2017
keywords: -OID_GEN_SUPPORTED_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 85295c8fdabfaacb1e8a8ea6c450f077079e95fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578867"
---
# <a name="oidgensupportedlist"></a>OID\_GEN\_サポートされている\_一覧


クエリ、OID として\_GEN\_サポートされている\_一覧 OID、ミニポート ドライバーまたは NIC をサポートするオブジェクトの Oid の配列を指定します。 オブジェクトには、[全般]、メディア固有および実装に固有のオブジェクトが含まれます。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。 参照してください[OID\_GEN\_サポートされている\_一覧 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff560258)します。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。 参照してください[OID\_GEN\_サポートされている\_一覧 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff560258)します。

<a name="remarks"></a>コメント
-------

NDIS 6.0 とそれ以降のミニポート ドライバーでは、この OID 要求は表示されません。 NDIS は、ミニポート ドライバーが初期化中に指定するキャッシュされた値を持つこの OID を処理します。

NDIS は、このクエリを行うプロトコル ドライバーに指定されたリストのサブセットを転送します。 つまり、プロトコル ドライバーの統計情報のクエリを行うことはありませんので、NDIS は、リストからサポートされている統計 Oid をフィルター処理します。

ミニポート ドライバーには、サポートされている Oid 一覧に OID が一覧表示する場合、OID を完全にサポートする必要があります。 つまり、ミニポート ドライバーでは、クエリに応答するときに、有効なデータを返すか oid には、リスト内に含まれる要求を設定する必要があります。 たとえば、 [OID\_GEN\_統計](oid-gen-statistics.md)OID は、NDIS 6.0 とそれ以降のミニポート ドライバーの必要な OID。 ミニポート ドライバーでは、ハードウェアまたはソフトウェアの統計情報をサポートしていませんし、不適切な統計情報を返します場合、ドライバーは、OID を指定できません\_GEN\_サポートされている Oid 一覧内の統計。

重複部分は、サポートされている Oid 一覧に表示可能性があります。 ドライバーは、一覧には、各 OID の 1 つのエントリがあることを保証する必要はありません。

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


[OID\_GEN\_統計情報](oid-gen-statistics.md)

 

 




