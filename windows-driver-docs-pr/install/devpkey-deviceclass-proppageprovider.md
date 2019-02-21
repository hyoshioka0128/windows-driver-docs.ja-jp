---
title: DEVPKEY_DeviceClass_PropPageProvider
description: DEVPKEY_DeviceClass_PropPageProvider
ms.assetid: 467a050e-9dd4-4b3b-a942-ee29667ac264
keywords:
- DEVPKEY_DeviceClass_PropPageProvider デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_PropPageProvider
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 230483f81e72dbcdc197f760c59be1d3eaf8b1e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550742"
---
# <a name="devpkeydeviceclassproppageprovider"></a>DEVPKEY_DeviceClass_PropPageProvider


DEVPKEY_DeviceClass_PropPageProvider デバイス プロパティがプロパティ ページのプロバイダーを表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_PropPageProvider</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データ形式</strong></p></td>
<td align="left"><p>&quot;<em>プロパティ プロバイダー</em>.dll、<em>プロバイダー エントリ ポイント</em>&quot;</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>EnumPropPages32</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_DeviceClass_PropPageProvider の値は、の値、 **EnumPropPages32**クラスのレジストリ キーの下のレジストリ値。 この値には、デバイス セットアップ クラスのクラスのプロパティのページ プロバイダーの DLL と、プロバイダーのエントリ ポイントの名前が含まれています。

**EnumPropPages32**のデバイス セットアップ クラスに対するレジストリ値を設定できます、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)に含まれている、 [ **INFClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)のクラスをインストールする INF ファイル。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するにはPropPageProvider します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_PropPageProvider プロパティのキーをサポートしていません。 このプロパティの値をアクセスするには、対応するのにアクセスして**EnumPropPages32**クラスのレジストリ キーの下のレジストリ値。 クラスのレジストリ キー値のエントリをアクセスする方法については、次を参照してください。[にアクセスするレジストリ エントリの値で、クラス レジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff537751)します。

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


[**INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 






