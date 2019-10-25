---
title: ファイルのハンドルを開く
description: ファイルのハンドルを開く
ms.assetid: 9378282a-ee29-44b6-b206-602eee94ec3b
keywords:
- ファイル WDK カーネル
- ファイルオブジェクト WDK カーネル
- オブジェクト WDK ファイルオブジェクト
- ファイルが WDK カーネルを処理する
- WDK カーネルファイルへのハンドル
- ファイルへのハンドルを開いています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b47def9148f071e3fcc59e01f5054b060b702eb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827738"
---
# <a name="opening-a-handle-to-a-file"></a>ファイルのハンドルを開く





ファイルへのハンドルを開くには、次の手順を実行します。

1.  [**オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_object_attributes)構造体を作成し、 [**initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)マクロを呼び出して構造体を初期化します。 ファイルのオブジェクト名は、 **Initializeobjectattributes**に対する*ObjectName*パラメーターとして指定します。

2.  **オブジェクト\_ATTRIBUTES**構造体を[**iocreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)、 [**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)、または[**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)に渡すことによって、ファイルへのハンドルを開きます。

    ファイルが存在しない場合は、 **iocreatefile**と**zwcreatefile**によって作成されますが、 **zwcreatefile**は状態\_オブジェクト\_\_名前を返し\_見つかりませんでした。

ドライバーは、ほとんどの場合、 **iocreatefile**ではなく**zwcreatefile**または**zwcreatefile**を使用することに注意してください。

**Iocreatefile**、 **zwcreatefile**、または**zwcreatefile**を呼び出すと、Windows executive はファイルを表す新しいファイルオブジェクトを作成し、オブジェクトを開くハンドルを提供します。 このファイルオブジェクトは、開いているハンドルをすべて閉じるまで保持されます。

どちらのルーチンを呼び出す場合でも、必要なアクセス権を*DesiredAccess*パラメーターとして渡す必要があります。 これらの権限は、ドライバーが実行するすべての操作に対応している必要があります。 次の表に、これらの操作と、それに対応するアクセス権を要求する方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>必要なアクセス権</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ファイルから読み取ります。</p></td>
<td><p>FILE_READ_DATA または GENERIC_READ</p></td>
</tr>
<tr class="even">
<td><p>ファイルに書き込みます。</p></td>
<td><p>FILE_WRITE_DATA または GENERIC_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>ファイルの末尾にのみ書き込みます。</p></td>
<td><p>FILE_APPEND_DATA</p></td>
</tr>
<tr class="even">
<td><p>ファイルの作成時刻など、ファイルのメタデータを読み取ります。</p></td>
<td><p>FILE_READ_ATTRIBUTES または GENERIC_READ</p></td>
</tr>
<tr class="odd">
<td><p>ファイルの作成時刻など、ファイルのメタデータを書き込みます。</p></td>
<td><p>FILE_WRITE_ATTRIBUTES または GENERIC_WRITE</p></td>
</tr>
</tbody>
</table>

 

*DesiredAccess*で使用できる値の詳細については、「 [**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)」を参照してください。

 

 




