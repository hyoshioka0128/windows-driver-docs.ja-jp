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
ms.openlocfilehash: 262c3c24e75ace510ae0da5030392c5494c83c75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355160"
---
# <a name="guiddevinterfacewriteoncedisk"></a>GUID_DEVINTERFACE_WRITEONCEDISK


GUID_DEVINTERFACE_WRITEONCEDISK[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)書き込みが定義されている、デバイスを 1 回ディスクします。

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

システム提供[記憶装置ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)オペレーティング システムと書き込みの存在をアプリケーションに通知する GUID_DEVINTERFACE_WRITEONCEDISK のインスタンスを登録などの CD-R ディスク 1 回

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

 

 






