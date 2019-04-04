---
title: DEVPKEY_Device_PDOName
description: DEVPKEY_Device_PDOName
ms.assetid: 1f2bc1e0-a671-47f6-9fbb-d0482b5abeca
keywords:
- DEVPKEY_Device_PDOName デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PDOName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d4e75e7f404371e31a008e388f02b465dbc1bd69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532071"
---
# <a name="devpkeydevicepdoname"></a>DEVPKEY_Device_PDOName


DEVPKEY_Device_PDOName デバイス プロパティは、デバイスのインスタンスを表す物理デバイス オブジェクト (PDO) の名前を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_PDOName</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_PHYSICAL_DEVICE_OBJECT_NAME</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows では、デバイスを表す物理名オブジェクト (PDO) の名前に DEVPKEY_Device_PDOName の値を設定します。 PDO 名の詳細については、次を参照してください。、 *DeviceName*パラメーターと共に使用される、 [ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)ルーチン。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_PDOName の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_PDOName プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_PHYSICAL_DEVICE_OBJECT_NAME 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)を参照してください。

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


[**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






