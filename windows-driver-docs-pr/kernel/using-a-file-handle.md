---
title: ファイル ハンドルを使用してください。
description: ファイル ハンドルを使用してください。
ms.assetid: f5a4d3f6-b74f-411e-9fa9-a41d83152fd7
keywords:
- ファイルの WDK カーネル
- ファイル オブジェクトの WDK カーネル
- WDK のオブジェクトのファイル オブジェクト
- ファイル ハンドルの WDK カーネル
- ファイルの WDK カーネルへのハンドルします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6898283ebcacc5c43631a0c6887ef396326c1a3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535624"
---
# <a name="using-a-file-handle"></a>ファイル ハンドルを使用してください。





次の表は、ドライバーは、ファイル ハンドルとそれらの操作を実行する対応するルーチンで実行できる操作を一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>呼び出すルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ファイルからデータを読み取ります。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567072" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567072)"><strong>ZwReadFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>データ ファイルを書き込みます。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567121" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567121)"><strong>ZwWriteFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>ファイルまたはファイル ハンドルのメタデータを読み取る。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567052" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567052)"><strong>ZwQueryInformationFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>ファイルまたはファイル ハンドルのメタデータを記述します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567096" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567096)"><strong>ZwSetInformationFile</strong></a></p></td>
</tr>
</tbody>
</table>

 

渡すを読み取りやデータの書き込みを開始するファイルの場所を示すために、 *ByteOffset*パラメーターを**ZwReadFile**または**ZwWriteFile**、それぞれします。

ファイル ハンドルを開いた場合\_追加\_データ アクセス、すべてのデータは、ファイルの末尾に記述された、 *ByteOffset*パラメーターは無視されます。

特定の条件下では、I/O マネージャーは、ファイルの現在のファイル位置ポインターを保持します。 読み取りを開始したり、その位置にある操作を指定することで書き込み**NULL**の*ByteOffset*します。 詳細については、現在のファイル位置のポインターが存在するときに、次を参照してください。[ファイルの現在位置を使用して](using-the-current-file-position.md)このセクションで後述します。

調査または変更されたファイルに関する情報、呼び出す[ **ZwQueryInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567052)または[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)、それぞれします。 特定の種類の情報を指定する、 *FileInformationClass*各ルーチンへのパラメーター。 たとえば、設定*FileInformationClass*に**FileBasicInformation**を調査または変更することができます、 [**ファイル\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545762)構造体は、ファイル作成時刻と他のユーザーの間で最終アクセス日時のメンバーが含まれています。 すべての可能な値については*FileInformationClass*を参照してください[**ファイル\_情報\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff728840)します。

 

 




