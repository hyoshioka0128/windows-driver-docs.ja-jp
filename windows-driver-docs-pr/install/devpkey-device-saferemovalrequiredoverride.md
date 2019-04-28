---
title: DEVPKEY_Device_SafeRemovalRequiredOverride
description: DEVPKEY_Device_SafeRemovalRequiredOverride
ms.assetid: 8289effe-3849-41bf-b870-69e3d8cb8850
keywords:
- DEVPKEY_Device_SafeRemovalRequiredOverride デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SafeRemovalRequiredOverride
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a802b18e53834bd36ae655177f994ee920c05767
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380088"
---
# <a name="devpkeydevicesaferemovalrequiredoverride"></a>DEVPKEY_Device_SafeRemovalRequiredOverride


DEVPKEY_Device_SafeRemovalRequiredOverride デバイス プロパティは、デバイスのインスタンスの安全な取り外しオーバーライドを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_SafeRemovalRequiredOverride</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアクセス アプリケーションをインストールしてインストーラー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このデバイスのプロパティは、ヒューリスティックの結果にその Windows プラグをオーバーライドするために使用でき、の値を計算するプレイ (PnP) を使用して、 [ **DEVPKEY_Device_SafeRemovalRequired** ](devpkey-device-saferemovalrequired.md)デバイス プロパティ。 この上書きは、次のように実行されます。

-   DEVPROP_TRUE に DEVPKEY_Device_SafeRemovalRequiredOverride デバイスのプロパティを設定し、デバイス インスタンスが取り外し可能またはリムーバブル先祖、PnP セット DEVPROP_TRUE DEVPKEY_Device_SafeRemovalRequired デバイス プロパティを持つし、使用しない場合、ヒューリスティックです。

    **注**  デバイス インスタンスは、リムーバブル デバイスの機能が設定されている場合は、リムーバブルと見なされます。 詳細については、次を参照してください。[リムーバブル デバイスの機能の概要](https://msdn.microsoft.com/library/windows/hardware/ff549564)します。

     

-   DEVPROP_TRUE に DEVPKEY_Device_SafeRemovalRequiredOverride デバイスのプロパティを設定し、デバイスのインスタンス (または先祖である) がリムーバブル、PnP は、DEVPROP_FALSE を DEVPKEY_Device_SafeRemovalRequired に設定し、ヒューリスティックを使用しません。

-   場合 DEVPKEY_Device_SafeRemovalRequiredOverride デバイスのプロパティが設定か DEVPROP_FALSE に設定、PnP DEVPKEY_Device_SafeRemovalRequired デバイス プロパティ設定によって、ヒューリスティックを使用して決定される値にします。

DEVPKEY_Device_SafeRemovalRequiredOverride の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)します。 呼び出すことによってこの値を設定することもできます。 [ **SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)します。

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

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 






