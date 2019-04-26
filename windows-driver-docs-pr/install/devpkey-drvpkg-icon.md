---
title: DEVPKEY_DrvPkg_Icon
description: DEVPKEY_DrvPkg_Icon
ms.assetid: 30aa817c-9dda-4504-b51a-78ef91d0cf01
keywords:
- DEVPKEY_DrvPkg_Icon デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_Icon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03174c0f7843337bfd333921d34d130e73681972
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342363"
---
# <a name="devpkeydrvpkgicon"></a>DEVPKEY_DrvPkg_Icon


DEVPKEY_DrvPkg_Icon デバイス プロパティは、Windows はデバイスのインスタンスを視覚的に表現を使用してデバイス アイコンの一覧を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_Icon</p></td>
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
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>〇</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

リスト内の各アイコンがアイコン ファイルのパスで指定された (\*.ico) または実行可能ファイルのアイコンのリソースへの参照。

一覧の最初のアイコンは、既定値として使用されます。 デバイスのさまざまな視覚的な表現を提供する追加アイコンを指定できます。 Windows には、ユーザーが Windows のアイコンを表示する選択ユーザー インターフェイスが用意されています。 たとえば、Microsoft の DiscoveryCam 530 は青、緑、および赤で使用できます。 Microsoft では、それぞれの色のアイコンを提供します。 Windows では、一覧で 1 つ目のために、既定では青いアイコンを使用します。 ただし、Windows ユーザーには緑色のアイコンか赤いアイコンが選択もできます。

アイコンの一覧は、アイコンの指定子の NULL 文字で区切った一覧を示します。 アイコンの指定子は、いずれかのアイコン ファイルのパス (\*.ico)、または次のように、アイコン リソース指定子。

-   アイコン ファイルへのパスの形式は*DirectoryPath\\filename.ico します。*

-   アイコン リソースの指定子では、次のエントリがあります。

    ```cpp
    @executable-file-path,resource-identifier
    ```

    アイコン リソースの指定子の最初の文字は、アット マーク (@) 後に実行可能ファイルのパス (、  *\*.exe*または *\*.dll*ファイル)、その後にコンマ (,)、をクリックし、*リソース識別子*エントリ。

"アイコン指定子など、@shell32.dll,-30"実行可能ファイル"shell32.dll"と「-30」リソース識別子を表します。

リソース識別子は、次のように、実行可能ファイル内のリソースに対応する整数値である必要があります。

-   提供された識別子が負の場合、Windows は、提供された識別子の絶対値と等しい識別子を持つ実行可能ファイル内のリソースを使用します。

-   提供された識別子がゼロの場合、Windows は、識別子を持つ execuable ファイル内の最小値を持つ実行可能ファイルで、リソースを使用します。

-   提供された識別子が正の値、例では、値のかどうかは*n*Windows は、識別子を持つ、n + 1 内の最小値、実行可能ファイルは、実行可能ファイルにリソースを使用します。 たとえば場合の値*n*は 1 です。 Windows 実行可能ファイルで 2 番目に小さい値を持つファイル識別子を持つリソースを使用します。

DEVPKEY_DrvPkg_Icon によっての値を設定することができます、 [ **INF AddProperty ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546318)に含まれている、 [ **INF *DDInstall*セクション** ](https://msdn.microsoft.com/library/windows/hardware/ff547344)のデバイスをインストールする INF ファイル。 DEVPKEY_DrvPkg_Icon の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)します。

次に、INF を使用する方法の例**AddProperty** 、INF によってインストールされているデバイスに DEVPKEY_DrvPkg_Icon を設定するディレクティブ*DDInstall* "SampleDDInstallSection"のセクションします。

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceIcon,,,,"SomeResource.dll,-2","SomeIcon.icon"
...
```

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


[**INF AddProperty ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






