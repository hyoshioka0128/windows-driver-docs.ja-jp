---
title: DEVPKEY_Device_DeviceDesc
description: DEVPKEY_Device_DeviceDesc
ms.assetid: 02b88ee7-d825-48d9-99ef-aac8e6748141
keywords:
- DEVPKEY_Device_DeviceDesc デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DeviceDesc
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e9a4760eb3d4ccdc3c8ed4a651616804370f0142
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527576"
---
# <a name="devpkeydevicedevicedesc"></a>DEVPKEY_Device_DeviceDesc


DEVPKEY_Device_DeviceDesc デバイスのプロパティは、デバイスのインスタンスの記述を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DeviceDesc</p></td>
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
<td align="left"><p>SPDRP_DEVICEDESC</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>〇</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_DeviceDesc の値によって設定されます、*デバイス説明*エントリの値によって指定された、 [ **INF モデル セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)をインストールする INF ファイルのデバイスです。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_DEVICE_DeviceDesc の値を取得します。

値を取得することができます、 [ **DEVPKEY_NAME** ](devpkey-name--device-instance-.md)デバイス インスタンスのプロパティをユーザー インターフェイスの項目に表示する必要があります、デバイスの名前を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_DeviceDesc プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンは、プロパティの値へのアクセスに対応する SPDRP_DEVICEDESC 識別子を使用します。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)します。

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


[**DEVPKEY_NAME (デバイス インスタンス)**](devpkey-name--device-instance-.md)

[**INF モデル セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






