---
title: GUID_DEVINTERFACE_OPM
description: GUID_DEVINTERFACE_OPM
ms.assetid: bd999b09-d531-4b89-a306-83e1ca7cac64
keywords:
- GUID_DEVINTERFACE_OPM デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_OPM
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e8374b9a01e61e13da9b06482156b710f7cadf42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840634"
---
# <a name="guid_devinterface_opm"></a>GUID_DEVINTERFACE_OPM


GUID_DEVINTERFACE_OPM [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、 [Windows Vista ディスプレイドライバモデル](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)のコンテキストで動作し、子デバイスを監視するための出力保護管理 (OPM) をサポートするディスプレイアダプタドライバに対して定義されています。

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
<td align="left"><p>GUID_DEVINTERFACE_OPM</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{BF4672DE-6B4E-4BE4-A325-68A91EA49C09}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

ドライバーは、このデバイスインターフェイスクラスのインスタンスを登録して、オペレーティングシステムと、OPM デバイスインターフェイスの存在をアプリケーションに通知します。

ディスプレイミニポートドライバーがこの[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)の DIRECT call OPM インターフェイスをサポートしている場合、カーネルモードコンポーネントは、ミニポートドライバーの[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出し、GUID_DEVINTERFACE_OPM インターフェイスの種類を指定します。

OPM の詳細については、「 [Output Protection Manager のサポート](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-output-protection-manager)」を参照してください。

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

 

 





