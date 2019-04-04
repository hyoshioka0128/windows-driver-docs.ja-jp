---
title: DEVPKEY_Device_ModelId
description: DEVPKEY_Device_ModelId
ms.assetid: 6066f18b-40bf-4b36-9821-5e886e166256
keywords:
- DEVPKEY_Device_ModelId デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ModelId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f6fbf4b052a9d074e3e908725d155c1f5b265392
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580929"
---
# <a name="devpkeydevicemodelid"></a>DEVPKEY_Device_ModelId


DEVPKEY_Device_ModelId デバイスのプロパティに一致するデバイスを[デバイス メタデータ パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff541439)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ModelId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアクセス アプリケーションをインストールしてインストーラー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

DEVPKEY_Device_ModelId のデバイス プロパティでは、同じ製造元とモデルを共有するデバイスを一意に識別するには、Ihv および Oem のサポートを提供します。 モデル識別子 (ModelID) を使用すると、Oem および ihv 側は、独自のブランド化されたデバイス メタデータ パッケージを配布するデバイスのモデルを一致できます。

DEVPKEY_Device_ModelId のデバイス プロパティの値を格納、 [ **ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)デバイスのメタデータ パッケージの XML 要素。 デバイスがインストールされている場合、デバイスによって報告された ModelID GUID 値を持つこの鍵が設定されます。

詳細については、[デバイス メタデータ パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff541439)を参照してください。

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
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[デバイス メタデータ パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff541439)

[**ModelID**](https://msdn.microsoft.com/library/windows/hardware/ff549295)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






