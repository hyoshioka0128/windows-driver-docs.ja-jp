---
title: DEVPKEY_DeviceClass_SilentInstall
description: DEVPKEY_DeviceClass_SilentInstall
ms.assetid: db9ff5d2-020f-47bc-a1e3-2b305b5270e9
keywords:
- DEVPKEY_DeviceClass_SilentInstall デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_SilentInstall
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 64538de0a790da0db59c53b643457fd6a590c000
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532740"
---
# <a name="devpkeydeviceclasssilentinstall"></a>DEVPKEY_DeviceClass_SilentInstall


DEVPKEY_DeviceClass_SilentInstall デバイス プロパティはブール値をかどうかを制御するフラグでデバイスを[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)インストール必要がありますが、可能であれば、任意のユーザー インターフェイス項目を表示することがなく。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_SilentInstall</p></td>
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
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>SilentInstall</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_DeviceClass_SilentInstall の値が DEVPROP_TRUE に設定されている場合、Windows は、ドライバーがドライバー ストアに既にプレインストールされている場合は、すべてのユーザー インターフェイス項目を表示することがなくデバイスのドライバーをインストールします。 そうしないと、Windows では、ユーザー インターフェイスの項目の表示は表示しません。

**SilentInstall**のデバイス セットアップ クラスに対するレジストリ値を設定することができます、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)に含まれている、 [ **INFClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)のクラスをインストールする INF ファイル。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するにはSilentInstall します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_SilentInstall プロパティのキーをサポートしていません。 このプロパティの値をアクセスするには、対応するのにアクセスして**SilentInstall**クラスのレジストリ キーの下のレジストリ値。 クラスのレジストリ キー値のエントリをアクセスする方法については、[にアクセスするレジストリ エントリの値で、クラス レジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff537751)を参照してください。

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

 

 






