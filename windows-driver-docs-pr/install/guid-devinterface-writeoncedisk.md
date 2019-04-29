---
title: GUID_DEVINTERFACE_WRITEONCEDISK
description: GUID_DEVINTERFACE_WRITEONCEDISK
ms.assetid: 8b1660e1-0868-40aa-ba47-dfcb6cf58aaf
keywords:
- GUID_DEVINTERFACE_WRITEONCEDISK デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_WRITEONCEDISK
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3a8253d0da7eae155fac6142514700111e385adc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330924"
---
# <a name="guiddevinterfacewriteoncedisk"></a>GUID_DEVINTERFACE_WRITEONCEDISK


GUID_DEVINTERFACE_WRITEONCEDISK[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)書き込みが定義されている、デバイスを 1 回ディスクします。

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
<td align="left"><p>GUID_DEVINTERFACE_WRITEONCEDISK</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F5630C-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)オペレーティング システムと書き込みの存在をアプリケーションに通知する GUID_DEVINTERFACE_WRITEONCEDISK のインスタンスを登録などの CD-R ディスク 1 回

[**WriteOnceDiskClassGuid** ](writeoncediskclassguid.md) GUID_DEVINTERFACE_WRITEONCEDISK デバイス インターフェイスのクラスの古い識別子です。 このクラスの新しいインスタンスは、代わりに GUID_DEVINTERFACE_WRITEONCEDISK を使用します。

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
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WriteOnceDiskClassGuid**](writeoncediskclassguid.md)

 

 






