---
title: DEVPKEY_Device_Capabilities
description: DEVPKEY_Device_Capabilities
ms.assetid: 8bda0c77-b711-41a9-9feb-52b22de224f0
keywords:
- DEVPKEY_Device_Capabilities デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Capabilities
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d634cde53ceb1a4bc488476034dca05cd2c426e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527470"
---
# <a name="devpkeydevicecapabilities"></a>DEVPKEY_Device_Capabilities


DEVPKEY_Device_Capabilities デバイスのプロパティは、デバイスのインスタンスの機能を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Capabilities</p></td>
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
<td align="left"><p>SPDRP_CAPABILITIES</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows デバイス ドライバーへの応答を返す機能の値を DEVPKEY_Device_Capabilities の値の設定、 [ **IRP_MN_QUERY_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff551664)デバイスの機能の要求情報。 DEVPKEY_Device_Capabilities の値は、CM_DEVCAP_ のビットごとの OR*Xxx* Cfgmgr32.h で定義されている機能のフラグ。 これらのフラグを表すデバイスの機能がのメンバーのサブセットに対応して、 [ **DEVICE_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_Capabilities の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_Capabilities プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_CAPABILITIES 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)を参照してください。

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


[**DEVICE_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff543095)

[**IRP_MN_QUERY_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff551664)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






