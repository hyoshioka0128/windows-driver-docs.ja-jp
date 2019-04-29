---
title: ファイルを共有するパッケージ対応印刷ドライバー
description: ファイルを共有するパッケージ対応印刷ドライバー
ms.assetid: dcf4e7b4-f0f4-4644-9f5c-c01c1b6c4221
keywords:
- パッケージに対応した印刷ドライバー WDK
- core ドライバー WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e63c3910ee2f3615d5bac7293b4faad227a8b47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324222"
---
# <a name="package-aware-print-drivers-that-share-files"></a>ファイルを共有するパッケージ対応印刷ドライバー


1 つ以上の印刷ドライバー パッケージは、ドライバー ファイルを共有する場合は、コア ドライバーに共有ファイルを分離する必要があります。 たとえば、Unidrv は Unidrv はコア ドライバー、多くの印刷ドライバーを使用して、ファイルのコレクションです。

Unidrv では、Windows XP の INF ファイルの次のセクションで示すようにドライバーが使用ニーズと、INF ファイルのインクルード ディレクティブを印刷します。

```cpp
[UniDrvInstall]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD
DataSection=UNIDRV_DATA
Include=NTPRINT.INF
Needs=UNIDRV.OEM,TTFSUB.OEM
```

Windows Vista では、パッケージに対応したドライバーを新たに使用する必要があります**CoreDriverSections**キーワードに Windows Vista の INF ファイルの次のセクションで示すように、Unidrv ファイルを参照する場合。

```cpp
[UniDrvInstall_Vista]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD
CoreDriverSections="{D20EA372-DD35-4950-9ED8-A6335AFE79F0}, 
 UNIDRV.OEM, UNIDRV_DATA, TTFSUB.OEM"
```

Windows Vista では、Unidrv はコア ドライバーとしてパッケージ化し、は、グローバル一意識別子 (GUID) で参照するため Ntprint.inf への参照は必要ありません。 Core のドライバーを使用する場合は使用しないでください、 **DataSection**キーワードが代わりにこのセクションを参照して、 **CoreDriverSections**キーワード。

印刷のパッケージのコア ファイルは、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コア ファイル</th>
<th>GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UNIDRV</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F0}</p></td>
</tr>
<tr class="even">
<td><p>PSCRIPT</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F1}</p></td>
</tr>
<tr class="odd">
<td><p>PCLXL</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F2}</p></td>
</tr>
<tr class="even">
<td><p>プロッター</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F4}</p></td>
</tr>
<tr class="odd">
<td><p>XPSDRV</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F5}</p></td>
</tr>
</tbody>
</table>

 

1 つ以上のコアとなるドライバー セクションを参照できます。例えば：

```cpp
CoreDriverSections="{GUID1}, SectionName1, SectionName2", "{GUID2}, SectionName3"
```

コア ドライバーに依存するドライバーをインストールするときに、印刷のインストーラーはドライバー ストアにその中核となるドライバーの最新バージョンを検索し、最新バージョンがインストールされます。

ここでは、次のトピックについて説明します。

[書き込みコア ドライバー](writing-core-drivers.md)

[Core のドライバーを使用します。](using-core-drivers.md)

[Core のドライバーのサンプル](core-driver-sample.md)

 

 




