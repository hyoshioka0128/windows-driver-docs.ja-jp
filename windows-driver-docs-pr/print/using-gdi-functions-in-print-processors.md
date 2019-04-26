---
title: プリント プロセッサで GDI 関数を使用する
description: プリント プロセッサで GDI 関数を使用する
ms.assetid: 2ad62308-ab42-4475-ac42-f753d5091251
keywords:
- EMF レコード再生 WDK プリント プロセッサ
- GDI 関数 WDK のプリント プロセッサ
- NT EMF WDK のプリント プロセッサ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9d512cd7f12f6e3929f1994f00bb5a945c551b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339918"
---
# <a name="using-gdi-functions-in-print-processors"></a>プリント プロセッサで GDI 関数を使用する





一連のユーザー モードの GDI 関数は、入力の形式として EMF NT-ベースのオペレーティング システムを処理するプリント プロセッサによって使用される Gdi32.dll、によってエクスポートされます。 次の表では、用意されている機能を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549449" data-raw-source="[&lt;strong&gt;GdiDeleteSpoolFileHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549449)"><strong>GdiDeleteSpoolFileHandle</strong></a></p></td>
<td><p>スプール ファイル ハンドルを解放します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549463" data-raw-source="[&lt;strong&gt;GdiEndDocEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549463)"><strong>GdiEndDocEMF</strong></a></p></td>
<td><p>印刷ドキュメントの EMF 再生操作を完了します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549468" data-raw-source="[&lt;strong&gt;GdiEndPageEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549468)"><strong>GdiEndPageEMF</strong></a></p></td>
<td><p>、物理ページの EMF 再生操作が完了して、プリンターからページを取り出します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549470" data-raw-source="[&lt;strong&gt;GdiGetDC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549470)"><strong>GdiGetDC</strong></a></p></td>
<td><p>プリンターのデバイス コンテキストへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549478" data-raw-source="[&lt;strong&gt;GdiGetDevmodeForPage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549478)"><strong>GdiGetDevmodeForPage</strong></a></p></td>
<td><p>ドキュメントのページを返します<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549492" data-raw-source="[&lt;strong&gt;GdiGetPageCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549492)"><strong>GdiGetPageCount</strong></a></p></td>
<td><p>ドキュメントのページの数を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549505" data-raw-source="[&lt;strong&gt;GdiGetPageHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549505)"><strong>GdiGetPageHandle</strong></a></p></td>
<td><p>ドキュメントのページへのハンドルを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549517" data-raw-source="[&lt;strong&gt;GdiGetSpoolFileHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549517)"><strong>GdiGetSpoolFileHandle</strong></a></p></td>
<td><p>その他の GDI 関数への入力として必要なスプール ファイル ハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549524" data-raw-source="[&lt;strong&gt;GdiPlayPageEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549524)"><strong>GdiPlayPageEMF</strong></a></p></td>
<td><p>ドキュメントのページに関連付けられた EMF レコードを再生します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549529" data-raw-source="[&lt;strong&gt;GdiResetDCEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549529)"><strong>GdiResetDCEMF</strong></a></p></td>
<td><p>プリンターのデバイス コンテキストをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549534" data-raw-source="[&lt;strong&gt;GdiStartDocEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549534)"><strong>GdiStartDocEMF</strong></a></p></td>
<td><p>印刷ジョブのドキュメントの初期化の操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549543" data-raw-source="[&lt;strong&gt;GdiStartPageEMF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549543)"><strong>GdiStartPageEMF</strong></a></p></td>
<td><p>物理ページの初期化の操作を実行します。</p></td>
</tr>
</tbody>
</table>

 

EMF、プリント プロセッサの[ **PrintDocumentOnPrintProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff560724)呼び出す必要があります[ **GdiGetSpoolFileHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff549517)スプール ファイルを取得するには処理と[ **GdiGetDC** ](https://msdn.microsoft.com/library/windows/hardware/ff549470)プリンターのデバイス コンテキスト ハンドルを取得します。 次の手順を実行できます。

-   各印刷ジョブ ドキュメントの[ **GdiStartDocEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549534) EMF レコードが再生される前に呼び出す必要があると[ **GdiEndDocEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549463)必要があります最後の EMF レコードが再生された後に呼び出されます。

-   印刷するには、[各物理ページの[ **GdiStartPageEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549543) ] ページで、任意のドキュメント ページの描画前に呼び出す必要があると[ **GdiEndPageEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549468)ドキュメントの最後のページが物理ページに描画された後に呼び出す必要があります。

-   各ドキュメントのページ、物理ページ上に描画されます[ **GdiGetDevmodeForPage** ](https://msdn.microsoft.com/library/windows/hardware/ff549478) DEVMODE 構造体の内容がドキュメントの最後のページの描画後に変更されたかどうかを判断を呼び出す必要があります。 DEVMODE が変更された場合、新しい物理ページが開始する必要があります (呼び出して[ **GdiEndPageEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549468)と[ **GdiStartPageEMF**](https://msdn.microsoft.com/library/windows/hardware/ff549543))、およびプリンターのデバイス コンテキストを呼び出すことによって更新する必要があります[ **GdiResetDCEMF**](https://msdn.microsoft.com/library/windows/hardware/ff549529)します。 最初の呼び出しによってドキュメントのページが物理ページに描画される[ **GdiGetPageHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff549505)ドキュメント ページのハンドルと、呼び出し元を取得する[ **GdiPlayPageEMF**](https://msdn.microsoft.com/library/windows/hardware/ff549524)ページを描画するためにします。

ジョブが完全に描画された後、プリント プロセッサを呼び出す必要があります[ **GdiDeleteSpoolFileHandle**](https://msdn.microsoft.com/library/windows/hardware/ff549449)します。

呼び出すことができます (逆の順序でページを印刷する場合など) の印刷ページを開始する前にプリント プロセッサの合計ページ数が必要な場合[ **GdiGetPageCount**](https://msdn.microsoft.com/library/windows/hardware/ff549492)、までこの関数を返しませんが、スプールが終了し、したがってスプール中に印刷する機能を無効にします。

プリント プロセッサは、これらの GDI 関数を使用している場合、 [ **EnumPrintProcessorDatatypes** ](https://msdn.microsoft.com/library/windows/hardware/ff548757)関数がサポートされているデータ型、汎用の Windows 2000 以降の EMF 形式を表すとして"NT EMF"を返す必要があります。 プリント プロセッサは、EMF レコードを変更する必要があります。

 

 




