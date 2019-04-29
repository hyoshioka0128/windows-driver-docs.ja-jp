---
title: DEVPKEY_Device_DriverVersion
description: DEVPKEY_Device_DriverVersion
ms.assetid: 68df1313-e948-4aea-9b90-c838f7bf228d
keywords:
- DEVPKEY_Device_DriverVersion デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverVersion
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b7418965cee5edc6f2c65626ff113af4980c9cbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330912"
---
# <a name="devpkeydevicedriverversion"></a>DEVPKEY_Device_DriverVersion


PKEY_Device_DriverVersion デバイス プロパティは、デバイスのインスタンスに現在インストールされているドライバーのバージョンを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DriverVersion</p></td>
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
<td align="left"><p><strong>対応するレジストリ値の識別子とレジストリ値の名前</strong></p></td>
<td align="left"><p>REGSTR_VAL_DRIVERVERSION</p>
<p><strong>driverVersion</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

DEVPKEY_Device_DriverVersion の値がによって提供される、 [ **INF DriverVer ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547394)に含まれている、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)がデバイスをインストールまたは特定のデバイス INF によって提供される INF ファイルの**DriverVer**ディレクティブに含まれている、 [ **INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)デバイスをインストールします。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) PKEY_Device_DriverVersion の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_DriverVersion プロパティのキーをサポートしていません。 この以前のバージョンの Windows で、対応するアクセスすることでこのプロパティの値にアクセスできます**DriverVersion**ソフトウェア キーをデバイス インスタンスの下のレジストリ値。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス ドライバーのプロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537732)します。

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


[**INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**INF DriverVer Directive**](https://msdn.microsoft.com/library/windows/hardware/ff547394)

[**バージョンの INF セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






