---
title: DEVPKEY_Device_Characteristics
description: DEVPKEY_Device_Characteristics
ms.assetid: 148557aa-2246-4cd9-9008-d920ffb64845
keywords:
- DEVPKEY_Device_Characteristics デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Characteristics
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 473610537721d2af040b98b8a347fb5781e6f95b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573694"
---
# <a name="devpkeydevicecharacteristics"></a>DEVPKEY_Device_Characteristics


DEVPKEY_Device_Characteristics デバイスのプロパティは、デバイスのインスタンスの特性を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Characteristics</p></td>
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
<td align="left"><p>SPDRP_CHARACTERISTICS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

DEVPKEY_Device_Characteristics の値が、これはのビットごとの OR*Xxx*ファイル Wdm.h と Ntddk.h で定義されている特性のフラグ。 デバイスの特性フラグの詳細については、次を参照してください、 *DeviceCharacteristics*パラメーターの[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)と[を指定する。デバイスの特性](https://msdn.microsoft.com/library/windows/hardware/ff563818)します。

使用して DEVPKEY_Device_Characteristics の値を設定することができます、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)に含まれている、 [ **INF DDInstall.HW セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)デバイスをインストールします。

DEVPKEY_Device_Characteristics の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_Characteristics プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_CHARACTERISTICS 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)します。

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


[**INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF DDInstall.HW セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)

[**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 






