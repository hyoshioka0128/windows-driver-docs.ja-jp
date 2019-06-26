---
title: GUID_DEVINTERFACE_PARALLEL
description: GUID_DEVINTERFACE_PARALLEL
ms.assetid: 3c7c27ba-aad6-4ca5-ba26-fba206f967b9
keywords:
- GUID_DEVINTERFACE_PARALLEL デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_PARALLEL
api_location:
- Ntddpar.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f8c4f86938f72d321bc4538d483ba48ce0f5e57e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386430"
---
# <a name="guiddevinterfaceparallel"></a>GUID_DEVINTERFACE_PARALLEL


GUID_DEVINTERFACE_PARALLEL[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[パラレル ポート](https://docs.microsoft.com/previous-versions/ff544263(v=vs.85))IEEE 1284 と互換性のあるハードウェア インターフェイスをサポートします。

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
<td align="left"><p>GUID_DEVINTERFACE_PARALLEL</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{97F76EF0-F883-11D0-AF1F-0000F800845C}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

パラレル ポート用のドライバーでは、オペレーティング システムおよびパラレル ポートの存在をアプリケーションに通知する GUID_DEVINTERFACE_PARALLEL のインスタンスを登録します。

パラレル ポートのシステムによって提供される関数のドライバーでは、パラレル ポートの場合は、このデバイス クラスのインスタンスを登録します。

並列デバイスとドライバーについては、次を参照してください。[パラレル ポートやデバイスの概要](https://docs.microsoft.com/previous-versions/ff543964(v=vs.85))します。

パラレル ポートに接続されているデバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_PARCLASS**](guid-devinterface-parclass.md)します。

[**GUID_PARALLEL_DEVICE** ](guid-parallel-device.md)このデバイス インターフェイス クラスの古い形式の識別子は、このクラスの新しいインスタンスが GUID_DEVINTERFACE_PARALLEL を代わりに使用します。

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
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddpar.h (Ntddpar.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_PARCLASS**](guid-devinterface-parclass.md)

[**GUID_PARALLEL_DEVICE**](guid-parallel-device.md)

 

 






