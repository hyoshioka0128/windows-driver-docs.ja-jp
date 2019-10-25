---
title: ファイル ハンドルの使用
description: ファイル ハンドルの使用
ms.assetid: f5a4d3f6-b74f-411e-9fa9-a41d83152fd7
keywords:
- ファイル WDK カーネル
- ファイルオブジェクト WDK カーネル
- オブジェクト WDK ファイルオブジェクト
- ファイルが WDK カーネルを処理する
- WDK カーネルファイルへのハンドル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfddc7ec8ab6985db575b397a7a9ac5d95085756
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836055"
---
# <a name="using-a-file-handle"></a>ファイル ハンドルの使用





次の表に、ファイルハンドルでドライバーが実行できる操作とそれらの操作を実行する対応ルーチンを示します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)"><strong>ZwReadFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>ファイルにデータを書き込みます。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)"><strong>ZwWriteFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>ファイルハンドルまたはファイルハンドルのメタデータを読み取ります。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)"><strong>ZwQueryInformationFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>ファイルハンドルまたはファイルハンドルのメタデータを書き込みます。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)"><strong>ZwSetInformationFile</strong></a></p></td>
</tr>
</tbody>
</table>

 

ファイル内でデータの読み取りまたは書き込みを開始する場所を指定するには、それぞれ、 *Byteoffset*パラメーターを**zwreadfile**または**zwreadfile**に渡します。

ファイル\_のハンドルを開いて\_データアクセスを追加した場合、すべてのデータがファイルの末尾に書き込まれ、 *Byteoffset*パラメーターは無視されます。

特定の条件下では、i/o マネージャーがファイルの現在のファイル位置ポインターを保持します。 *Byteoffset*に**NULL**を指定することで、その位置で読み取りまたは書き込み操作を開始できます。 現在のファイル位置ポインターが存在する場合の詳細については、このセクションで後述する「[現在のファイルの位置を使用](using-the-current-file-position.md)する」を参照してください。

ファイルに関する情報を確認または変更するには、それぞれ[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)または[**zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)を呼び出します。 各ルーチンの*Fileinformationclass*パラメーターとして、特定の種類の情報を指定します。 たとえば、 *Fileinformationclass*を**fileinformationclass**に設定すると、ファイル作成時のメンバーと最後のアクセス権を含む[**ファイル\_基本的な\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)構造を確認または変更できます。それ以外の時間。 *Fileinformationclass*で使用可能なすべての値については、「[**ファイル\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)」を参照してください。

 

 




