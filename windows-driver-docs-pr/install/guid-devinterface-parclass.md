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
ms.openlocfilehash: ab08bb06e662e97bc956d7d5dfca21228f4810fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363698"
---
# <a name="guiddevinterfaceparclass"></a>GUID_DEVINTERFACE_PARCLASS


GUID_DEVINTERFACE_PARCLASS[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)にアタッチされているデバイスが定義されている、[パラレル ポート](https://msdn.microsoft.com/library/windows/hardware/ff544263)します。

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

並列デバイスとドライバーについては、次を参照してください。[並列のデバイス デザイン ガイド](https://msdn.microsoft.com/library/windows/hardware/ff544263)します。

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

 

 






