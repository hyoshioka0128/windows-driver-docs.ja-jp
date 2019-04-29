---
title: DEVPKEY_Device_PowerRelations
description: DEVPKEY_Device_PowerRelations
ms.assetid: 616e6d02-9047-491b-b7e7-758e1804dff5
keywords:
- DEVPKEY_Device_PowerRelations デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PowerRelations
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7de658f66d005123dcd2179762100a7c5fd5b543
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327222"
---
# <a name="devpkeydevicepowerrelations"></a>DEVPKEY_Device_PowerRelations


DEVPKEY_Device_PowerRelations デバイス プロパティを表します、 [**リレーションの電源を**](https://msdn.microsoft.com/library/windows/hardware/ff551670)デバイス インスタンス。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_PowerRelations</p></td>
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
<td align="left"><p>該当なし</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_PowerRelations の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティを直接サポートされません。 以前のバージョンの Windows でのデバイスのリレーションのプロパティを取得する方法については、次を参照してください。[デバイス関係の取得](https://msdn.microsoft.com/library/windows/hardware/ff550630)します。

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

 

 






