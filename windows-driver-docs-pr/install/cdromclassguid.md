---
title: CdRomClassGuid
description: CdRomClassGuid
ms.assetid: 406c28c9-8ef3-4ccc-bb70-a13b8d1ad64e
keywords:
- CdRomClassGuid デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- CdRomClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 91a246f2734fc1d4d118ef26015a2ae4eaa79d1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537997"
---
# <a name="cdromclassguid"></a>CdRomClassGuid


CdRomClassGuid は古い形式の識別子、[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)CD-ROM の[記憶装置](https://msdn.microsoft.com/library/windows/hardware/ff566969)します。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_CDROM** ](guid-devinterface-cdrom.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK で含める、 [CDROM クラス ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256093)サンプルと[Addfilter ストレージ フィルター ツール](https://go.microsoft.com/fwlink/p/?linkid=256076)。 CDROM クラス ドライバーのサンプルでは、CdRomClassGuid を使用して、GUID_DEVINTERFACE_CDROM デバイス インターフェイスのクラスのインスタンスを登録します。 サンプルの Addfilter アプリケーションでは、CdRomClassGuid を使用して、GUID_DEVINTERFACE_CDROM デバイス インターフェイスのクラスのインスタンスを列挙します。

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
<td align="left"><p>使われていません。 Windows 2000 以降、GUID_DEVINTERFACE_CDROM を代わりに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)

 

 






