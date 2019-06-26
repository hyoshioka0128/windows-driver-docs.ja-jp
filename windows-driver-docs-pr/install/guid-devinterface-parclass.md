---
title: GUID_DEVINTERFACE_PARCLASS
description: GUID_DEVINTERFACE_PARCLASS
ms.assetid: d55195d4-f4f5-464f-a1ca-5fe0eafccb2a
keywords:
- GUID_DEVINTERFACE_PARCLASS デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_PARCLASS
api_location:
- Ntddpar.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f7d2a6e95e3105dd679c8afe400ec4e9f80e005c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386431"
---
# <a name="guiddevinterfaceparclass"></a>GUID_DEVINTERFACE_PARCLASS


GUID_DEVINTERFACE_PARCLASS[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)にアタッチされているデバイスが定義されている、[パラレル ポート](https://docs.microsoft.com/previous-versions/ff544263(v=vs.85))します。

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
<td align="left"><p>GUID_DEVINTERFACE_PARCLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{811FC6A5-F728-11D0-A537-0000F8753ED1}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

パラレル ポートに接続されている並列のデバイス用のドライバーでは、オペレーティング システムとアプリケーションの並列のデバイスの存在を通知する GUID_DEVINTERFACE_PARCLASS のインスタンスを登録します。

パラレル ポートのシステム提供のバス ドライバーでは、パラレル ポートに接続されているハードウェア デバイスごとにこのデバイスのインターフェイス クラスのインスタンスを作成します。

並列デバイスとドライバーについては、次を参照してください。[並列のデバイス デザイン ガイド](https://docs.microsoft.com/previous-versions/ff544263(v=vs.85))します。

パラレル ポート、デバイス インターフェイスのクラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_PARALLEL**](guid-devinterface-parallel.md)します。

[**GUID_PARCLASS_DEVICE** ](guid-parclass-device.md)このデバイス インターフェイス クラスの古い形式の識別子は、このクラスの新しいインスタンスが GUID_DEVINTERFACE_PARCLASS を代わりに使用します。

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


[**GUID_DEVINTERFACE_PARALLEL**](guid-devinterface-parallel.md)

[**GUID_PARCLASS_DEVICE**](guid-parclass-device.md)

 

 






