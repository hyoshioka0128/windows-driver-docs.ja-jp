---
title: GUID_DEVINTERFACE_BRIGHTNESS
description: GUID_DEVINTERFACE_BRIGHTNESS
ms.assetid: a31b4e12-3702-4a24-98c0-cf8ae7d86a75
keywords:
- GUID_DEVINTERFACE_BRIGHTNESS デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_BRIGHTNESS
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 519315cf1c00d4e3d2e0561821bd671f4de6daee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342059"
---
# <a name="guiddevinterfacebrightness"></a>GUID_DEVINTERFACE_BRIGHTNESS


GUID_DEVINTERFACE_BRIGHTNESS[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)のコンテキストで動作するディスプレイ アダプター ドライバーが定義されている、 [Windows Vista のディスプレイ ドライバー モデル](https://msdn.microsoft.com/library/windows/hardware/ff570593)と輝度のサポート子デバイスを監視します。

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
<td align="left"><p>GUID_DEVINTERFACE_BRIGHTNESS</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{FDE5BBA4-B3F9-46FB-BDAA-0728CE3100B4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

ドライバーは、オペレーティング システムや子デバイスを監視の明るさコントロール インターフェイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

ディスプレイのミニポート ドライバーは、この直接呼出しの明るさコントロールのインターフェイスをサポートしている場合[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)、カーネル モード コンポーネントを呼び出して、ミニポート ドライバーの直接呼び出しインターフェイスを取得できます[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)関数とインターフェイスの種類を指定する GUID_DEVINTERFACE_BRIGHTNESS を指定します。

明るさのデバイスについては、次を参照してください。[統合表示パネルの明るさコントロールをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff569755)と[明るさコントロール インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff538260)します。

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
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h (Dispmprt.h を含む)</td>
</tr>
</tbody>
</table>

 

 





