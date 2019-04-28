---
title: DEVPKEY_Device_InstanceId
description: DEVPKEY_Device_InstanceId
ms.assetid: 74c78289-e140-46da-8005-ef6f441f78ec
keywords:
- DEVPKEY_Device_InstanceId デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_InstanceId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d78f6e52ed5966ff8a9bd751b522f365470172fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380749"
---
# <a name="devpkeydeviceinstanceid"></a>DEVPKEY_Device_InstanceId


DEVPKEY_Device_InstanceId デバイス プロパティは、デバイスのデバイスのインスタンス識別子を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_InstanceId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって読み取り専用アクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_InstanceId の値が、デバイスのインスタンスのインストール中に Windows によって内部的に設定されます。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)デバイス インスタンスの DEVPKEY_Device_InstanceId の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_InstanceId プロパティのキーをサポートしていません。 Windows の以前のバージョンのデバイスのインスタンス識別子を取得する方法については、次を参照してください。[デバイス インスタンス Id を取得する](https://msdn.microsoft.com/library/windows/hardware/ff549863)します。

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


[**SetupDiGetDeviceInstanceId**](https://msdn.microsoft.com/library/windows/hardware/ff551106)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






