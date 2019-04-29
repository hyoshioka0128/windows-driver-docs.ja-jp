---
title: GUID_DEVINTERFACE_CDCHANGER
description: GUID_DEVINTERFACE_CDCHANGER
ms.assetid: 9bcbe3d5-2057-44cb-a495-6edee14a9cbb
keywords:
- GUID_DEVINTERFACE_CDCHANGER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_CDCHANGER
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 778b30c2851a202ff79b538825f07b22f5a50c6c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383680"
---
# <a name="guiddevinterfacecdchanger"></a>GUID_DEVINTERFACE_CDCHANGER


GUID_DEVINTERFACE_CDCHANGER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)チェンジャーの CD-ROM デバイスに対して定義されています。

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
<td align="left"><p>GUID_DEVINTERFACE_CDCHANGER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F56312-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供の CD-ROM[チェンジャー ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff551455)オペレーティング システムとチェンジャーの CD-ROM デバイスの存在をアプリケーションに通知する GUID_DEVINTERFACE_CDCHANGER のインスタンスを登録します。

CD-ROM デバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)します。

記憶域デバイスについては、次を参照してください。[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)します。

[**CdChangerClassGuid** ](cdchangerclassguid.md) GUID_DEVINTERFACE_CDCHANGER デバイス インターフェイス クラスの古い形式の識別子は、このクラスの新しいインスタンスが GUID_DEVINTERFACE_CDCHANGER を代わりに使用します。

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
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CdChangerClassGuid**](cdchangerclassguid.md)

[**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)

 

 






