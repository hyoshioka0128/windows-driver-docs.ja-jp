---
title: DEVPKEY_Device_FirstInstallDate
description: DEVPKEY_Device_FirstInstallDate
ms.assetid: aedc4f18-51be-4c42-a172-c1fd88cc49b3
keywords:
- DEVPKEY_Device_FirstInstallDate デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_FirstInstallDate
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c8196ea108cccd16758330b6a29cbca59c6b92b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380761"
---
# <a name="devpkeydevicefirstinstalldate"></a>DEVPKEY_Device_FirstInstallDate


DEVPKEY_Device_FirstInstallDate デバイスのプロパティは、システム内のデバイスのインスタンスを初めてインストールしたときに、タイムスタンプを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_FirstInstallDate</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-filetime.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_FILETIME&lt;/strong&gt;](devprop-type-filetime.md)"><strong>DEVPROP_TYPE_FILETIME</strong></a></p></td>
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

Windows では、デバイス インスタンスが最初に、システムでインストールされを指定するタイムスタンプを持つ DEVPKEY_Device_FirstInstallDate の値を設定します。

**注**  とは異なり、 [ **DEVPKEY_Device_InstallDate** ](devpkey-device-installdate.md)プロパティ、連続する各更新プログラムと DEVPKEY_Device_FirstInstallDate プロパティの値は変更されませんデバイス ドライバー。 たとえば、Windows Update で更新されたドライバーが、このプロパティの値を変更できません。

 

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_FirstInstallDate プロパティの値を取得します。

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
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






