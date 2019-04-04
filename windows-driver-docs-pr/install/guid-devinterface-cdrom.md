---
title: GUID_DEVINTERFACE_CDROM
description: GUID_DEVINTERFACE_CDROM
ms.assetid: ecc31c09-27f5-4a80-8aa6-adc70d8a76c3
keywords:
- GUID_DEVINTERFACE_CDROM デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_CDROM
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dac56719f1334916bda5c00089210247317bc87e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570880"
---
# <a name="guiddevinterfacecdrom"></a>GUID_DEVINTERFACE_CDROM


GUID_DEVINTERFACE_CDROM[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)CD-ROM が定義されている[記憶装置](https://msdn.microsoft.com/library/windows/hardware/ff566969)します。

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
<td align="left"><p>GUID_DEVINTERFACE_CDROM</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F56308-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

CD-ROM の記憶域デバイスのシステム指定のクラス ドライバーは、オペレーティング システムと CD-ROM デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK で含める、 [CDROM クラス ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256093)サンプルと[Addfilter ストレージ フィルター ツール](https://go.microsoft.com/fwlink/p/?linkid=256076)。 CD-ROM クラス ドライバーのサンプルが古い形式の識別子を使用して[ **CdRomClassGuid** ](cdromclassguid.md) GUID_DEVINTERFACE_CDROM デバイス インターフェイスのクラスのインスタンスを登録します。 サンプルの Addfilter アプリケーションでは、CdRomClassGuid を使用して、GUID_DEVINTERFACE_CDROM デバイス インターフェイスのクラスのインスタンスを列挙します。

チェンジャーの CD-ROM デバイスに対するデバイスのインターフェイス クラスについては、[ **GUID_DEVINTERFACE_CDCHANGER**](guid-devinterface-cdchanger.md)を参照してください。

記憶域デバイスについては、[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CdRomClassGuid**](cdromclassguid.md)

[**GUID_DEVINTERFACE_CDCHANGER**](guid-devinterface-cdchanger.md)

 

 






