---
title: GUID_DEVINTERFACE_WPD
description: GUID_DEVINTERFACE_WPD
ms.assetid: 611d1866-2530-4acb-8c83-77c29bdd128c
keywords:
- GUID_DEVINTERFACE_WPD デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_WPD
api_location:
- Portabledevice.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2260f30e0b6d1bf026cbed3298bdaea1a2b95bcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370007"
---
# <a name="guiddevinterfacewpd"></a>GUID_DEVINTERFACE_WPD


GUID_DEVINTERFACE_WPD[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている[Windows ポータブル デバイス](https://go.microsoft.com/fwlink/p/?linkid=106527)(WPD)。

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
<td align="left"><p>GUID_DEVINTERFACE_WPD</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{6AC27878-A6FA-4155-BA85-F98F491D4F33}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

WPD デバイス ドライバー インターフェイス (DDI) をサポートしているデバイスのドライバーでは、WPD デバイスが存在する、オペレーティング システムとアプリケーションに通知する GUID_DEVINTERFACE_WPD のインスタンスを登録します。

WPD クラスの拡張機能コンポーネントは、WPD クラスの拡張機能を使用する WPD ドライバーの場合は、このデバイス インターフェイスのインスタンスを登録します。

WPD デバイスを使用するクライアントは、このデバイスのインターフェイス クラスのインスタンスの到着を通知を受ける必要があります。

クライアントが呼び出すことによってこのインターフェイスを登録する WPD デバイスを列挙できる**IPortableDeviceManager::GetDevices** (Windows SDK に記載されている)。

プライベート WPD デバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_WPD_PRIVATE**](guid-devinterface-wpd-private.md)します。

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
<td align="left"><p>Windows Vista、Windows XP、および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Portabledevice.h (Portabledevice.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_WPD_PRIVATE**](guid-devinterface-wpd-private.md)

 

 






