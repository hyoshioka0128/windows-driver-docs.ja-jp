---
title: GUID_DEVINTERFACE_DISK
description: GUID_DEVINTERFACE_DISK
ms.assetid: 47782789-4504-4705-8c32-4d2bc508a7e2
keywords:
- GUID_DEVINTERFACE_DISK デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_DISK
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c31927d862e23fb9bba327eb97f9dfed1f8627b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342302"
---
# <a name="guiddevinterfacedisk"></a>GUID_DEVINTERFACE_DISK


GUID_DEVINTERFACE_DISK[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)ハード ディスクが定義されている[記憶装置](https://msdn.microsoft.com/library/windows/hardware/ff566969)します。

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
<td align="left"><p>GUID_DEVINTERFACE_DISK</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F56307-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

システムが指定したストレージ クラス ドライバーは、ハード_ディスクの記憶域デバイスに対する GUID_DEVINTERFACE_DISK のインスタンスを登録します。

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK で含める、[ディスク クラス ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256103)サンプルと[Addfilter ストレージ フィルター ツール](https://go.microsoft.com/fwlink/p/?linkid=256076)。 ディスクのクラス ドライバーのサンプルが古い形式の識別子を使用して[ **DiskClassGuid** ](diskclassguid.md) GUID_DEVINTERFACE_DISK デバイス インターフェイスのクラスのインスタンスを登録します。 サンプルの Addfilter アプリケーションでは、DiskClassGuid を使用して、GUID_DEVINTERFACE_DISK デバイス インターフェイス クラスのインスタンスを列挙します。

ストレージ ドライバーについては、次を参照してください。[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)します。

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


[**DiskClassGuid**](diskclassguid.md)

 

 






