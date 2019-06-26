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
ms.openlocfilehash: c4464c1d50e8bb3c4f21cb73fc93479c7d2b7888
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387327"
---
# <a name="guidavcclass"></a>GUID_AVC_CLASS


GUID_AVC_CLASS[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)でサポートされているオーディオ ビデオ コントロール (AV/C) デバイスが定義されている、 [AVStream](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)アーキテクチャ。

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

システム提供[AV/C クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-client-drivers2) [Avc.sys](https://docs.microsoft.com/windows-hardware/drivers/stream/using-avc-sys) 1394 バス上の外部の AV/C 単位を表す GUID_AVC_CLASS のインスタンスを登録します。

AV/C の仮想デバイスのデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)します。

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

 

 






