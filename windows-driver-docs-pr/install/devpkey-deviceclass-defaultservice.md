---
title: DEVPKEY_DeviceClass_DefaultService
description: DEVPKEY_DeviceClass_DefaultService
ms.assetid: 19d1a9ea-3bde-4230-af1a-b67b5a29e6f4
keywords:
- DEVPKEY_DeviceClass_DefaultService デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DefaultService
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8158f5e9d97425b19d3765a647520873b2e9d20f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530373"
---
# <a name="devpkeydeviceclassdefaultservice"></a>DEVPKEY_DeviceClass_DefaultService


DEVPKEY_DeviceClass_DefaultService のデバイス プロパティの既定のサービスの名前を表します、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_DefaultService</p></td>
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
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>既定のサービス</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

デバイス セットアップ クラスに対する既定のサービスがインストールされているし、デバイスがデバイスに固有のサービスをインストールしていない場合、 [ **INF ClassInstall32.Services セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546339)のクラスをインストールする INF ファイルデバイスのクラスの既定のサービスをインストールします。

DEVPKEY_DeviceClass_DefaultService の値は、の値、**既定 Service**クラスのレジストリ キーの下のレジストリ値。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するにはDefaultService します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_DefaultService プロパティのキーをサポートしていません。 対応するこのプロパティの値にアクセスすることができます**既定 Service**クラスのレジストリ キーの下のレジストリ値。 クラスのレジストリ キー値のエントリをアクセスする方法については、次を参照してください。[にアクセスするレジストリ エントリの値で、クラス レジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff537751)します。

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


[**INF ClassInstall32.Services セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546339)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 






