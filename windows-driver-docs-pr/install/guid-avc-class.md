---
title: GUID_AVC_CLASS
description: GUID_AVC_CLASS
ms.assetid: 1aa323d3-7d68-4c50-af68-01bda3792fec
keywords:
- GUID_AVC_CLASS デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_AVC_CLASS
api_location:
- Avc.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d73ce771cb4dbfe2eefbd0dcab57e3790c55a5b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557686"
---
# <a name="guidavcclass"></a>GUID_AVC_CLASS


GUID_AVC_CLASS[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)でサポートされているオーディオ ビデオ コントロール (AV/C) デバイスが定義されている、 [AVStream](https://msdn.microsoft.com/library/windows/hardware/ff554240)アーキテクチャ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>GUID_AVC_CLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{095780C3-48A1-4570-BD95-46707F78C2DC}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供[AV/C クライアント ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff556367) [Avc.sys](https://msdn.microsoft.com/library/windows/hardware/ff568667) 1394 バス上の外部の AV/C 単位を表す GUID_AVC_CLASS のインスタンスを登録します。

AV/C の仮想デバイスのデバイスのインターフェイス クラスについては、[ **GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista、Windows Server 2003、Windows XP および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Avc.h (include Avc.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)

 

 






