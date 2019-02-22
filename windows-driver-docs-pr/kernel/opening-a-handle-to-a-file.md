---
title: ファイル ハンドルを開く
description: ファイル ハンドルを開く
ms.assetid: 9378282a-ee29-44b6-b206-602eee94ec3b
keywords:
- ファイルの WDK カーネル
- ファイル オブジェクトの WDK カーネル
- WDK のオブジェクトのファイル オブジェクト
- ファイル ハンドルの WDK カーネル
- ファイルの WDK カーネルへのハンドルします。
- ファイルへのハンドルを開く
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f8c3d475e4bb5e282794b3b9ed3deb426abc768
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531033"
---
# <a name="opening-a-handle-to-a-file"></a>ファイル ハンドルを開く





ファイルを識別するハンドルを開くには、次の手順に従います。

1.  作成、 [**オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff557749)構造体、および呼び出し、 [ **InitializeObjectAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff547804)初期化するためにマクロ構造体。 ファイルのオブジェクトの名前を指定する、 *ObjectName*パラメーターを**InitializeObjectAttributes**します。

2.  渡すことによって、ファイルへのハンドルを開く、**オブジェクト\_属性**構造体を[ **IoCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff548418)、 [ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)、または[ **ZwOpenFile**](https://msdn.microsoft.com/library/windows/hardware/ff567011)します。

    ファイルが存在しない場合**IoCreateFile**と**ZwCreateFile**は、作成**ZwOpenFile**状態を返す\_オブジェクト\_名前\_いない\_が見つかりました。

ドライバーをほとんど使用**ZwCreateFile**または**ZwOpenFile**なく**IoCreateFile**します。

呼び出すと**IoCreateFile**、 **ZwCreateFile**、または**ZwOpenFile**Windows executive をファイルを表す新しいオブジェクトを作成するやを開いているハンドルを提供しますオブジェクト。 すべての開いているハンドルを閉じるまで、このファイル オブジェクトが永続化します。

呼び出すと、どのルーチンとして必要なアクセス権を渡す必要があります、 *DesiredAccess*パラメーター。 これらの権利には、すべての操作には、ドライバーを実行する必要がありますについて説明します。 次の表は、要求するには、これらの操作と対応するアクセス権を示します。

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
<td><p>ファイルを読み取る&#39;ファイルなど、メタデータ&#39;作成時刻。</p></td>
<td><p>FILE_READ_ATTRIBUTES または GENERIC_READ</p></td>
</tr>
<tr class="odd">
<td><p>ファイルを書き込む&#39;ファイルなど、メタデータ&#39;作成時刻。</p></td>
<td><p>FILE_WRITE_ATTRIBUTES または GENERIC_WRITE</p></td>
</tr>
</tbody>
</table>

 

使用できる値の詳細については*DesiredAccess*を参照してください[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)します。

 

 




