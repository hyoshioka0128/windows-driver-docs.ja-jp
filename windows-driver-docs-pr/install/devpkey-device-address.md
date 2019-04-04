---
title: DEVPKEY_Device_Address
description: DEVPKEY_Device_Address
ms.assetid: 48951b9e-0bd0-4f56-9a6f-e8a5aa6c25c2
keywords:
- DEVPKEY_Device_Address デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Address
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b6dc47f9f3298612cc82c1ef2f6801d9109a558
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571639"
---
# <a name="devpkeydeviceaddress"></a>DEVPKEY_Device_Address


DEVPKEY_Device_Address デバイス プロパティは、デバイスのインスタンスのバスに固有のアドレスを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Address</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

Windows では、そのバス上のデバイスのアドレスに DEVPKEY_Device_Address の値を設定します。 デバイスのアドレスの解釈については、次を参照してください、 **DevicePropertyAddress**の値、 *DeviceProperty*パラメーターの[ **IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_Address の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_Address プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_ADDRESS 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)を参照してください。

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


[**IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






