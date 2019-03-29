---
title: DiskClassGuid
description: DiskClassGuid
ms.assetid: eeefc86c-caff-4d1c-b2c1-aefde3bd21ed
keywords:
- DiskClassGuid デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DiskClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0c1bed68dadb076ee1de4b1e368488f8e19ff9b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572155"
---
# <a name="diskclassguid"></a>DiskClassGuid


DiskClassGuid はハード ディスクのデバイスのインターフェイス クラスの識別子を廃止[記憶装置](https://msdn.microsoft.com/library/windows/hardware/ff566969)します。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_DISK** ](guid-devinterface-disk.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>コメント
-------

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK で含める、[ディスク クラス ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256103)サンプルと[Addfilter ストレージ フィルター ツール](https://go.microsoft.com/fwlink/p/?linkid=256076)。 ディスクのクラス ドライバーのサンプルでは、GUID_DEVINTERFACE_DISK デバイス インターフェイスのクラスのインスタンスを登録するのに DiskClassGuid を使用します。 サンプルの Addfilter アプリケーションでは、DiskClassGuid を使用して、GUID_DEVINTERFACE_DISK デバイス インターフェイスのクラスのインスタンスを列挙します。

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
<td align="left"><p>使われていません。 Windows 2000 以降、GUID_DEVINTERFACE_DISK を代わりに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_DISK**](guid-devinterface-disk.md)

 

 






