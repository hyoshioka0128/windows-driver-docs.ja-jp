---
title: GUID_DEVINTERFACE_VOLUME
description: GUID_DEVINTERFACE_VOLUME
ms.assetid: 34802df4-8a8f-48ea-a146-d2ad4ae4709a
keywords:
- GUID_DEVINTERFACE_VOLUME デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_VOLUME
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3e55c378c959995961562e15b127749a7b93bee5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573137"
---
# <a name="guiddevinterfacevolume"></a>GUID_DEVINTERFACE_VOLUME


GUID_DEVINTERFACE_VOLUME[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)ボリューム デバイス用に定義されます。

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
<td align="left"><p>GUID_DEVINTERFACE_VOLUME</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F5630D-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

システム提供[ストレージ クラス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff559215) GUID_DEVINTERFACE_VOLUME オペレーティング システムとアプリケーション ボリューム デバイスの存在の通知のインスタンスを登録します。 マウント マネージャでは、プラグ アンド プレイ (PnP) デバイス インターフェイスの通知メカニズムを使用して、到達またはボリューム インターフェイスの削除を通知します。

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK で含める、 [Addfilter ストレージ フィルター ツール](https://go.microsoft.com/fwlink/p/?linkid=256076)古い形式の識別子を使用する[ **VolumeClassGuid** ](volumeclassguid.md)GUID_DEVINTERFACE_VOLUME デバイス インターフェイス クラスのインスタンスを列挙します。

記憶装置ドライバーの詳細については、次を参照してください。[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)と[マウント マネージャーの要求、記憶域クラス ドライバーをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff567603)します。

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


[**VolumeClassGuid**](volumeclassguid.md)

 

 






