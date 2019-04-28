---
title: GUID_DEVINTERFACE_WPD_PRIVATE
description: GUID_DEVINTERFACE_WPD_PRIVATE
ms.assetid: 50292137-d648-41cf-928e-d72549f6321b
keywords:
- GUID_DEVINTERFACE_WPD_PRIVATE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_WPD_PRIVATE
api_location:
- Portabledevice.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9ffecf467ded2996a682634312c0ea684657af45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360598"
---
# <a name="guiddevinterfacewpdprivate"></a>GUID_DEVINTERFACE_WPD_PRIVATE


GUID_DEVINTERFACE_WPD_PRIVATE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)特殊化に対して定義されている[Windows ポータブル デバイス](https://go.microsoft.com/fwlink/p/?linkid=106527)(WPD)。

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
<td align="left"><p>GUID_DEVINTERFACE_WPD_PRIVATE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{BA0C718F-4DED-49B7-BDD3-FABE28661211}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

GUID_DEVINTERFACE_WPD_PRIVATE は、カスタムの WPD アプリケーションで使用されるプライベートのデバイスに対してのみ使用する必要があります。 ジェネリックの WPD ドライバーと WPD デバイスのクライアントでは、このデバイスのインターフェイス クラスのインスタンスを使用することはできません。

カスタム アプリケーションが呼び出すことによってこのインターフェイスを登録するプライベートのデバイスを列挙できる**IPortableDeviceManager::GetPrivateDevices** (Windows SDK に記載されている)。

汎用 WPD デバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_WPD**](guid-devinterface-wpd.md)します。

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
<td align="left"><p>Windows Vista、Windows XP、および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Portabledevice.h (Portabledevice.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_WPD**](guid-devinterface-wpd.md)

 

 






