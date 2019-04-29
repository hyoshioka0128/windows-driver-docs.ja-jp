---
title: GDI ファイル、モジュール、およびプロセス サービス
description: GDI ファイル、モジュール、およびプロセス サービス
ms.assetid: abf37bed-cad9-4fbc-95fe-346b0c07c81b
keywords:
- GDI WDK Windows 2000 の表示、モジュール サービス
- グラフィックス ドライバー WDK Windows 2000 の表示、モジュール サービス
- 描画 WDK GDI、モジュール サービス
- GDI WDK Windows 2000 の表示、ファイル サービス
- グラフィックス ドライバー WDK Windows 2000 の表示、ファイル サービス
- 描画 WDK GDI、ファイル サービス
- GDI WDK Windows 2000 の表示、プロセスのサービス
- WDK Windows 2000 を表示するグラフィック ドライバーは処理サービス
- WDK GDI を描画するには、サービスを処理します。
- プロセス サービスの WDK GDI
- ファイル サービスの WDK GDI
- WDK GDI モジュール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4613424238848cb3955b73f7724cfb17c11d7abe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385649"
---
# <a name="gdi-file-module-and-process-services"></a>GDI ファイル、モジュール、およびプロセス サービス


## <span id="ddk_gdi_file_module_and_process_services_gg"></span><span id="DDK_GDI_FILE_MODULE_AND_PROCESS_SERVICES_GG"></span>


GDI では、さまざまなファイル、モジュール、およびプロセス操作のサービスを提供します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564803" data-raw-source="[&lt;strong&gt;EngDeleteFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564803)"><strong>EngDeleteFile</strong></a></p></td>
<td align="left"><p>ファイルを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564865" data-raw-source="[&lt;strong&gt;EngFindImageProcAddress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564865)"><strong>EngFindImageProcAddress</strong></a></p></td>
<td align="left"><p>実行可能モジュール内の関数のアドレスを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564871" data-raw-source="[&lt;strong&gt;EngFindResource&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564871)"><strong>EngFindResource</strong></a></p></td>
<td align="left"><p>モジュール内のリソースの場所を決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564902" data-raw-source="[&lt;strong&gt;EngFreeModule&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564902)"><strong>EngFreeModule</strong></a></p></td>
<td align="left"><p>システム メモリからのファイルのマッピングを解除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564919" data-raw-source="[&lt;strong&gt;EngGetCurrentProcessId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564919)"><strong>EngGetCurrentProcessId</strong></a></p></td>
<td align="left"><p>現在のプロセスの ID を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564922" data-raw-source="[&lt;strong&gt;EngGetCurrentThreadId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564922)"><strong>EngGetCurrentThreadId</strong></a></p></td>
<td align="left"><p>現在のスレッドの ID を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564931" data-raw-source="[&lt;strong&gt;EngGetFileChangeTime&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564931)"><strong>EngGetFileChangeTime</strong></a></p></td>
<td align="left"><p>ファイルに最後に書き込んだ時刻を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564935" data-raw-source="[&lt;strong&gt;EngGetFilePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564935)"><strong>EngGetFilePath</strong></a></p></td>
<td align="left"><p>指定したフォント ファイルに関連付けられたファイルのパスを決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564955" data-raw-source="[&lt;strong&gt;EngGetProcessHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564955)"><strong>EngGetProcessHandle</strong></a></p></td>
<td align="left"><p>現在のクライアント プロセスを識別するハンドルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564963" data-raw-source="[&lt;strong&gt;EngLoadImage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564963)"><strong>EngLoadImage</strong></a></p></td>
<td align="left"><p>指定した実行可能イメージをカーネル モード メモリに読み込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564964" data-raw-source="[&lt;strong&gt;EngLoadModule&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564964)"><strong>EngLoadModule</strong></a></p></td>
<td align="left"><p>指定されたデータのモジュールを読み取り用のシステム メモリに読み込みます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564965" data-raw-source="[&lt;strong&gt;EngLoadModuleForWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564965)"><strong>EngLoadModuleForWrite</strong></a></p></td>
<td align="left"><p>指定された実行可能モジュールを書き込み用のシステム メモリに読み込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564971" data-raw-source="[&lt;strong&gt;EngMapFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564971)"><strong>EngMapFile</strong></a></p></td>
<td align="left"><p>作成またはファイルを開き、マップに<a href="https://msdn.microsoft.com/library/windows/hardware/ff556336#wdkgloss-system-space" data-raw-source="&lt;em&gt;system space&lt;/em&gt;"><em>システム領域</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564972" data-raw-source="[&lt;strong&gt;EngMapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564972)"><strong>EngMapFontFile</strong></a></p></td>
<td align="left"><p>使われていません。 このテーブルのエントリを参照してください。 <strong>EngMapFontFileFD</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564973" data-raw-source="[&lt;strong&gt;EngMapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564973)"><strong>EngMapFontFileFD</strong></a></p></td>
<td align="left"><p>必要に応じて、フォント ファイルをシステム メモリにマップし、ファイルでフォント データの基本の場所へのポインターを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564974" data-raw-source="[&lt;strong&gt;EngMapModule&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564974)"><strong>EngMapModule</strong></a></p></td>
<td align="left"><p>によって読み込まれている実行可能ファイルのサイズとアドレスを返します<strong>EngLoadModule</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564988" data-raw-source="[&lt;strong&gt;EngQueryFileTimeStamp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564988)"><strong>EngQueryFileTimeStamp</strong></a></p></td>
<td align="left"><p>ファイルのタイムスタンプを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565041" data-raw-source="[&lt;strong&gt;EngUnloadImage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565041)"><strong>EngUnloadImage</strong></a></p></td>
<td align="left"><p>によって読み込まれたイメージをアンロード<strong>EngLoadModule</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565437" data-raw-source="[&lt;strong&gt;EngUnmapFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565437)"><strong>EngUnmapFile</strong></a></p></td>
<td align="left"><p>ファイルのビューのマッピングを解除<a href="https://msdn.microsoft.com/library/windows/hardware/ff556336#wdkgloss-system-space" data-raw-source="&lt;em&gt;system space&lt;/em&gt;"><em>システム領域</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565441" data-raw-source="[&lt;strong&gt;EngUnmapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565441)"><strong>EngUnmapFontFile</strong></a></p></td>
<td align="left"><p>使われていません。 このテーブルのエントリを参照してください。 <strong>EngUnmapFontFileFD</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565445" data-raw-source="[&lt;strong&gt;EngUnmapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565445)"><strong>EngUnmapFontFileFD</strong></a></p></td>
<td align="left"><p>システム メモリから指定したフォント ファイルのマッピングを解除します。</p></td>
</tr>
</tbody>
</table>

 

 

 





