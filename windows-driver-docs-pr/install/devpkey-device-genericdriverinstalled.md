---
title: DEVPKEY_Device_GenericDriverInstalled
description: DEVPKEY_Device_GenericDriverInstalled
ms.assetid: 7809bed7-af11-42b0-bcc8-9492c47d92ab
keywords:
- DEVPKEY_Device_GenericDriverInstalled デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_GenericDriverInstalled
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 38e5e395340926b3902670efe6dc8f035f955a30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380754"
---
# <a name="devpkeydevicegenericdriverinstalled"></a>DEVPKEY_Device_GenericDriverInstalled


DEVPKEY_Device_GenericDriverInstalled デバイス プロパティは、デバイス インスタンス用にインストールされたドライバーがデバイスの基本機能のみを提供するかどうかを示すブール値を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_GenericDriverInstalled</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows では、DEVPKEY_Device_GenericDriverInstalled の値を設定します。

DEVPKEY_Device_GenericDriverInstalled の値は、基本的なドライバーがインストールされていることを示す DEVPROP_TRUE に設定されます。 それ以外の場合、プロパティの値は、DEVPROP_FALSE に設定されます。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_GenericDriverInstalled の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされません。

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

 

 






