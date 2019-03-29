---
title: GUID_VIRTUAL_AVC_CLASS
description: GUID_VIRTUAL_AVC_CLASS
ms.assetid: bd577fd7-f50c-4477-9619-8dd9e849367a
keywords:
- GUID_VIRTUAL_AVC_CLASS デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_VIRTUAL_AVC_CLASS
api_location:
- Avc.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6b757be14631fcd2da5b1b78b90457e59165b57f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581300"
---
# <a name="guidvirtualavcclass"></a>GUID_VIRTUAL_AVC_CLASS


GUID_VIRTUAL_AVC_CLASS[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)オーディオ ビデオ コントロール (AV/C) の仮想デバイスでサポートされているが定義されている、 [AVStream](https://msdn.microsoft.com/library/windows/hardware/ff554240)アーキテクチャ。

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
<td align="left"><p>GUID_VIRTUAL_AVC_CLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{616EF4D0-23CE-446D-A568-C31EB01913D0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

システム提供[AV/C クライアント ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff556367) [Avc.sys](https://msdn.microsoft.com/library/windows/hardware/ff568667)仮想 AV/C デバイスを表す GUID_VIRTUAL_AVC_CLASS のインスタンスを登録します。

1394 バス上の AV/C 単位デバイス インターフェイスのクラスについては、次を参照してください。 [ **GUID_AVC_CLASS**](guid-avc-class.md)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista、Microsoft Windows Server 2003、Windows XP および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Avc.h (include Avc.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_AVC_CLASS**](guid-avc-class.md)

 

 






