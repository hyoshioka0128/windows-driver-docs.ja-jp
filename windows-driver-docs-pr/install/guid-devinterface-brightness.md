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
ms.openlocfilehash: 2601f7bc73d3693205dd7b7ff82df411903f8798
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840632"
---
# <a name="guid_devinterface_brightness"></a>GUID_DEVINTERFACE_BRIGHTNESS


GUID_DEVINTERFACE_BRIGHTNESS [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、 [Windows Vista ディスプレイドライバモデル](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)のコンテキストで動作し、子デバイスを監視するための明るさ制御をサポートするディスプレイアダプタドライバに対して定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ID</p></td>
<td align="left"><p>GUID_DEVINTERFACE_BRIGHTNESS</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{FDE5BBA4-B3F9-46FB-BDAA-0728CE3100B4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

ドライバーは、このデバイスインターフェイスクラスのインスタンスを登録して、子デバイスを監視するための輝度制御インターフェイスがあることをオペレーティングシステムとアプリケーションに通知します。

ディスプレイミニポートドライバーがこの[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)の直接呼び出し輝度制御インターフェイスをサポートしている場合、カーネルモードコンポーネントはミニポートドライバーの[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)を呼び出すことによって、直接呼び出しインターフェイスを取得できます。インターフェイス型を指定するために GUID_DEVINTERFACE_BRIGHTNESS を提供します。

輝度デバイスの詳細については、「統合されたディスプレイパネルと[輝度コントロールインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)[での明るさの制御のサポート](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-brightness-controls-on-integrated-display-panels)」を参照してください。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Dispmprt (Dispmprt. h を含む)</td>
</tr>
</tbody>
</table>

 

 





