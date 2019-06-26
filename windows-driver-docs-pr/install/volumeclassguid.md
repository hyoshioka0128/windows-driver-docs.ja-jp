---
title: VolumeClassGuid
description: VolumeClassGuid
ms.assetid: 30d0db03-fbea-4245-b8d7-ca3a06a54861
keywords:
- VolumeClassGuid デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- VolumeClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c7d2684d127ace4921c38df7e238cac73619916e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380403"
---
# <a name="volumeclassguid"></a>VolumeClassGuid


VolumeClassGuid は古い形式の識別子、[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)ボリューム デバイスの場合。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_VOLUME** ](guid-devinterface-volume.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK で含める、 [Addfilter ストレージ フィルター ツール](https://go.microsoft.com/fwlink/p/?linkid=256076)VolumeClassGuid を使用してのインスタンスを列挙する、 [ **GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)デバイス インターフェイスのクラス。

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
<td align="left"><p>使われていません。 Windows 2000 以降、GUID_DEVINTERFACE_VOLUME を代わりに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

 

 






