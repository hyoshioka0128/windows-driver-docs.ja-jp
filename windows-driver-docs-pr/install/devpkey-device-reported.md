---
title: DEVPKEY_Device_Reported
description: DEVPKEY_Device_Reported
ms.assetid: dfec9e24-4d4e-42e4-a229-ad3d060fb1b5
keywords:
- DEVPKEY_Device_Reported デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Reported
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f81e4930f1c24138e635295ea67563b9c0273012
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573166"
---
# <a name="devpkeydevicereported"></a>DEVPKEY_Device_Reported


DEVPKEY_Device_Reported デバイスのプロパティは、デバイスのインスタンスがルート列挙のデバイスで、デバイスのドライバーがプラグ アンド プレイ (PnP) manager を呼び出すことによって報告されたかどうかを示すブール値を表します[ **IoReportDetectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549597)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Reported</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

PnP マネージャーでは、デバイスがデバイスのドライバーが呼び出し元 IoReportDetectedDevice によって PnP マネージャーに報告するルートで列挙されるデバイスの場合に、DEVPROP_TRUE に DEVPKEY_Device_Reported の値を設定します。 それ以外の場合、PnP マネージャーでは、DEVPROP_FALSE にプロパティの値を設定します。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_Reported の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされません。

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


[**IoReportDetectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549597)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






