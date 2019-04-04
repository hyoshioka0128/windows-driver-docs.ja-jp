---
title: DEVPKEY_Device_DriverInfSectionExt
description: DEVPKEY_Device_DriverInfSectionExt
ms.assetid: bf6260b4-5df3-4f85-8319-0f864c017e3d
keywords:
- DEVPKEY_Device_DriverInfSectionExt デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverInfSectionExt
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13d93e91e048e29f26cd0568805234906ce284e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560722"
---
# <a name="devpkeydevicedriverinfsectionext"></a>DEVPKEY_Device_DriverInfSectionExt


DEVPKEY_Device_DriverInfSectionExt デバイス ドライバーのプロパティは、のプラットフォームの拡張機能を表す、 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)デバイス インスタンス用のドライバーをインストールします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DriverInfSectionExt</p></td>
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
<td align="left"><p>REGSTR_VAL_INFSECTIONEXT</p>
<p><strong>InfSectionExt</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows では、DEVPKEY_Device_DriverInfSectionExt の値を設定します。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_DriverInfSectionExt の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_DriverInfSectionExt プロパティのキーをサポートしていません。 この以前のバージョンの Windows で、対応するアクセスすることでこのプロパティの値にアクセスできます**InfSectionExt**ソフトウェア キーをデバイス インスタンスの下のレジストリ値。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、[デバイス ドライバーのプロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537732)を参照してください。

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


[**INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






