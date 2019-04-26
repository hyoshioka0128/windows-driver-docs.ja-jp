---
title: DEVPKEY_Device_LegacyBusType
description: DEVPKEY_Device_LegacyBusType
ms.assetid: 76c2a472-bb05-4f6a-84da-0ae9e7c1fdf1
keywords:
- DEVPKEY_Device_LegacyBusType デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_LegacyBusType
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0828f29c7b3aa57d9f746ffde93b6110bb73b1de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351122"
---
# <a name="devpkeydevicelegacybustype"></a>DEVPKEY_Device_LegacyBusType


DEVPKEY_Device_LegacyBusType デバイス プロパティは、レガシ バスのデバイスのインスタンス数を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_LegacyBusType</p></td>
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
<td align="left"><p>SPDRP_LEGACYBUSTYPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

Windows の LegacyBusType メンバーの値に DEVPKEY_Device_LegacyBusType の値の設定、 [ **PNP_BUS_INFORMATION** ](https://msdn.microsoft.com/library/windows/hardware/ff559608)バス ドライバーへの応答を返す構造、 [**IRP_MN_QUERY_BUS_INFORMATION** ](https://msdn.microsoft.com/library/windows/hardware/ff551654)要求。 DEVPKEY_Device_LegacyBusType の値が 1 つの[ **INTERFACE_TYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff547839) Wdm.h と Ntddk.h で定義されている列挙子の値。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_LegacyBusType の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_LegacyBusType プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_LEGACYBUSTYPE 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)します。

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


[**INTERFACE_TYPE**](https://msdn.microsoft.com/library/windows/hardware/ff547839)

[**IRP_MN_QUERY_BUS_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff551654)

[**PNP_BUS_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff559608)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






