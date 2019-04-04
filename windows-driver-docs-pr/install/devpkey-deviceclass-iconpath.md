---
title: DEVPKEY_DeviceClass_IconPath
description: DEVPKEY_DeviceClass_IconPath
ms.assetid: c81ea18d-dd21-4b5e-8aba-52f7ad6931bf
keywords:
- DEVPKEY_DeviceClass_IconPath デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_IconPath
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c9585273aee84f3c1a01b6aff9ddf3246acfd62d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537886"
---
# <a name="devpkeydeviceclassiconpath"></a>DEVPKEY_DeviceClass_IconPath


DEVPKEY_DeviceClass_IconPath デバイス プロパティがのアイコンが一覧を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_IconPath</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>IconPath</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するにはIconPath します。

DEVPKEY_DeviceClass_IconPath 値は、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-Windows シェルによって使用される形式で、アイコン リソースの指定子の型指定されたリスト。 アイコン リソースの指定子の形式は"*ファイル パスの実行可能ファイル*、*リソース識別子*、"ここ*ファイル パスの実行可能ファイル*の完全修飾パスを含む、アイコン リソースを含むコンピューター上のファイルと*リソース識別子*リソースを識別する整数を指定します。 アイコン リソース指定子は、"%systemroot%\\system32\\DLL1.dll、-12"実行可能ファイルのパスが含まれています"%systemroot%\\system32\\DLL1.dll"と「-12」リソース識別子。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされません。 これらのバージョンの Windows のデバイス セットアップ クラスのアイコンの情報にアクセスする方法については、[デバイス セットアップ クラスのアイコンのプロパティにアクセスする](https://msdn.microsoft.com/library/windows/hardware/ff537746)を参照してください。

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


[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiLoadClassIcon**](https://msdn.microsoft.com/library/windows/hardware/ff552053)

 

 






