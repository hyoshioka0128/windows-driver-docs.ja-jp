---
title: DEVPKEY_DeviceClass_ClassName
description: DEVPKEY_DeviceClass_ClassName
ms.assetid: dc085e27-06c7-49ca-808f-3d1952cb8aa9
keywords:
- DEVPKEY_DeviceClass_ClassName デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_ClassName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e04770b53f2ecd8897963a2ab18faae4692632af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538421"
---
# <a name="devpkeydeviceclassclassname"></a>DEVPKEY_DeviceClass_ClassName


DEVPKEY_DeviceClass_ClassName デバイス プロパティのクラス名を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_ClassName</p></td>
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
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_DeviceClass_ClassName の値によって設定されます、**クラス**ディレクティブに含まれている、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547394)デバイス セットアップ クラスをインストールします。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するにはクラス名。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_ClassName プロパティのキーをサポートしていません。 Windows Server 2003、Windows XP、および Windows 2000 でのデバイス セットアップ クラスの名前にアクセスする方法については、次を参照してください。[フレンドリ名と、デバイス セットアップ クラスのクラス名にアクセスする](https://msdn.microsoft.com/library/windows/hardware/ff537755)します。

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


[**バージョンの INF セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547394)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiClassNameFromGuid**](https://msdn.microsoft.com/library/windows/hardware/ff550947)

 

 






