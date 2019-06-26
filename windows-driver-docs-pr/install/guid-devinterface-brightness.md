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
ms.openlocfilehash: ce9834404bbcd1972f92c1d0bfdfa365c229aa8a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370956"
---
# <a name="guiddevinterfacebrightness"></a>GUID_DEVINTERFACE_BRIGHTNESS


GUID_DEVINTERFACE_BRIGHTNESS[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)のコンテキストで動作するディスプレイ アダプター ドライバーが定義されている、 [Windows Vista のディスプレイ ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)と輝度のサポート子デバイスを監視します。

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

ディスプレイのミニポート ドライバーは、この直接呼出しの明るさコントロールのインターフェイスをサポートしている場合[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)、カーネル モード コンポーネントを呼び出して、ミニポート ドライバーの直接呼び出しインターフェイスを取得できます[ **DxgkDdiQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数とインターフェイスの種類を指定する GUID_DEVINTERFACE_BRIGHTNESS を指定します。

明るさのデバイスについては、次を参照してください。[統合表示パネルの明るさコントロールをサポートしている](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-brightness-controls-on-integrated-display-panels)と[明るさコントロール インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

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

 

 





