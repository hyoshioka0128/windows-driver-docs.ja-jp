---
title: DEVPKEY_Device_BusRelations
description: DEVPKEY_Device_BusRelations
ms.assetid: 590cbf77-3cee-4c74-bad1-ca237986cff0
keywords:
- DEVPKEY_Device_BusRelations デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BusRelations
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d04713f9a99dd388e96faad05af956e25b83c809
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573484"
---
# <a name="devpkeydevicebusrelations"></a>DEVPKEY_Device_BusRelations


DEVPKEY_Device_BusRelations デバイス プロパティを表します、 [**バス関係**](https://msdn.microsoft.com/library/windows/hardware/ff551670)デバイス インスタンス。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_BusRelations</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>適用なし</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_BusRelations の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティを直接サポートされません。 以前のバージョンの Windows でのデバイスのリレーションのプロパティを取得する方法については、次を参照してください。[デバイス関係の取得](https://msdn.microsoft.com/library/windows/hardware/ff550630)します。

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
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






