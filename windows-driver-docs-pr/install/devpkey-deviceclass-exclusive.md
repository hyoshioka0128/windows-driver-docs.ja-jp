---
title: DEVPKEY_DeviceClass_Exclusive
description: DEVPKEY_DeviceClass_Exclusive
ms.assetid: a05ada91-6a6f-4253-aca5-0740294a5c24
keywords:
- DEVPKEY_DeviceClass_Exclusive デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Exclusive
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4f3a2575e2586d767c7ca2118119a2f4bde5c9af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577847"
---
# <a name="devpkeydeviceclassexclusive"></a>DEVPKEY_DeviceClass_Exclusive


DEVPKEY_DeviceClass_Exclusive デバイス プロパティがかどうかのデバイスがのメンバーであるかを示すブール フラグを表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)は排他的なデバイスです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_Exclusive</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>インストール アプリケーションおよびデバイス セットアップ クラスをインストールした後、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_EXCLUSIVE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

インストール アプリケーションは、デバイス セットアップ クラスをインストールするときは、DEVPKEY_DeviceClass_Exclusive の値を設定できます。 デバイス セットアップ クラスと、このプロパティの設定をインストールする方法については、次を参照してください[ **INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)レジストリ値に関する情報と**排他。** で提供されている、"特殊な*値のエントリ名*キーワード"のセクション[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するには排他。

Windows Server 2003 および Windows XP は、このプロパティをサポートは DEVPKEY_DeviceClass_Exclusive プロパティのキーをサポートしていません。 この以前のバージョンの Windows では、このプロパティの値にアクセスするのに SPCRP_EXCLUSIVE 識別子を使用できます。 このプロパティの値にアクセスする方法については、[デバイス セットアップ クラス SPCRP_Xxx のプロパティを取得する](https://msdn.microsoft.com/library/windows/hardware/ff550644)を参照してください。

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

[**INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 






