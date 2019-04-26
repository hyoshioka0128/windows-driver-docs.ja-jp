---
title: MSBuild 用の WDK タスク
description: Windows Driver Kit (WDK) には、ビルド プロセスでよく使用されますが、Visual Studio では正常に配布されていないツールが含まれています。
ms.assetid: 53A5AAC2-A608-4153-9482-D8EF3D05EF04
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c41a5ae6821997fef5d49809758b4105b929236
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358082"
---
# <a name="wdk-tasks-for-msbuild"></a>MSBuild 用の WDK タスク


Windows Driver Kit (WDK) には、ビルド プロセスでよく使用されますが、Visual Studio では正常に配布されていないツールが含まれています。 これらのツールは、ドライバーまたはドライバー パッケージの署名には、ソフトウェアのトレースを実装するか、処理 (stampinf.exe、mc.exe、tracewpp.exe、binplace.exe など) は、リソースまたはメッセージのファイルをコンパイルに使用されます。 これらのコマンド ライン ツールは、ビルド プロセス中に実行できるようにする MSBuild タスク (ターゲットに含まれます) として公開する必要があります。 WDK は、ドライバーをビルドするときに、MSBuild タスクとしてこれらのツールを実行できるように、必要なコンポーネントを提供します。

**注**  ここに記載されている、WDK ツールは、通常、ビルド プロセスで使用してが WDK とドライバーの開発に役立つツールに含まれるツールの完全な一覧については、MSBuild タスクを参照してください、 [Windows のインデックスDriver Kit ツール](index-of-windows-driver-kit-tools.md)します。

 

WDK のコマンド ライン ツールでは、多数のオプションをサポートします。 各オプションは、タスクのパラメーターとして公開されます。 タスクが実行時にプロジェクト ファイルからも入力を受信できます。 MSBuild では、タスクを実行する直前にこれらのプロパティを設定します。 これらの個々 の WDK タスク ラッパー クラスは、プロジェクト ファイルでこれらのタスクの入力と出力パラメーターとして使用できる .NET プロパティを作成します。

## <a name="span-idtoolsthathavewdktasksspanspan-idtoolsthathavewdktasksspanspan-idtoolsthathavewdktasksspantools-that-have-wdk-tasks"></a><span id="Tools_that__have_WDK_Tasks"></span><span id="tools_that__have_wdk_tasks"></span><span id="TOOLS_THAT__HAVE_WDK_TASKS"></span>WDK のタスクがあるツール


次の表は、ツールと対応するタスク、ターゲット、およびアイテムの名前を示します。

| ツール名    | タスク名 | ターゲット名    | 項目の名前      |
|--------------|-----------|----------------|----------------|
| Tracewpp.exe | Wpp       | RunWpp         | ClCompile      |
| StampInf.exe | StampInf  | StampInf       | inf            |
| Mofcomp.exe  | mofcomp   | mofcomp        | mofcomp        |
| Wmimofck.exe | Wmimofck  | Wmimofck       | Wmimofck       |
| mc.exe       | Mc        | MessageCompile | MessageCompile |
| Ctrpp.exe    | Ctrpp     | Ctrpp          | Ctrpp          |

 

次の例では、ツールを呼び出す方法を示します。

```XML
<ItemGroup>
    <ClCompile Include="a.c" />
    <ClCompile Include="b.c">
        <WppEnabled>true</WppEnabled>
    </ClCompile>
</ItemGroup>
```

上記の例を呼び出す**tracewpp.exe**ファイル**b.c**コマンドを発行した場合、 **tracewpp.exe b.c**します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="tracewpp-task.md" data-raw-source="[TraceWPP task](tracewpp-task.md)">TraceWPP タスク</a></p></td>
<td align="left"><p>WDK には、MSBuild を使用してドライバーをビルドするときに、tracewpp.exe ツールを実行できるようにの TraceWPP タスクが用意されています。 Tracewpp.exe ツールが実装するために使用される<a href="wpp-software-tracing.md" data-raw-source="[WPP Software Tracing](wpp-software-tracing.md)">WPP ソフトウェア トレース</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="stampinf-task.md" data-raw-source="[Stampinf task](stampinf-task.md)">Stampinf タスク</a></p></td>
<td align="left"><p>WDK には、MSBuild を使用してドライバーをビルドするときに、stampinf.exe ツールを実行できるようにの StampInf タスクが用意されています。 Stampinf.exe ツールについては、次を参照してください。 <a href="stampinf.md" data-raw-source="[Stampinf](stampinf.md)">Stampinf</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wmimofck-task.md" data-raw-source="[Wmimofck task](wmimofck-task.md)">Wmimofck タスク</a></p></td>
<td align="left"><p>WDK には、MSBuild を使用して、ドライバーをビルドするときに、wmimofck.exe ツールを実行できるようにの Wmimofck タスクが用意されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="mofcomp-task.md" data-raw-source="[Mofcomp task](mofcomp-task.md)">Mofcomp タスク</a></p></td>
<td align="left"><p>WDK には、MSBuld を使用してドライバーをビルドするときに、Mofcomp.exe ツールを実行できるようにの Mofcomp にタスクが用意されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="message-compiler-task.md" data-raw-source="[Message compiler task](message-compiler-task.md)">メッセージ コンパイラ タスク</a></p></td>
<td align="left"><p>WDK には、MSBuild を使用してドライバーをビルドするときに、MC.exe ツールを実行できるようにの MessageCompiler タスクが用意されています。 MC.exe を使用する方法の詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/desktop/aa385638" data-raw-source="[&lt;strong&gt;Message Compiler (MC.exe)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa385638)"><strong>メッセージ コンパイラ (MC.exe)</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ctrpp-task.md" data-raw-source="[Ctrpp task](ctrpp-task.md)">Ctrpp タスク</a></p></td>
<td align="left"><p>WDK には、MSBuild を使用してドライバーをビルドするときに、ctrpp.exe ツールを実行できるようにの Ctrpp タスクが用意されています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**CTRPP**](https://msdn.microsoft.com/library/windows/desktop/aa372128)

[Wmimofck.exe を使用します。](https://msdn.microsoft.com/library/windows/hardware/ff565588)

[**メッセージ コンパイラ (MC.exe)**](https://msdn.microsoft.com/library/windows/desktop/aa385638)

[**mofcomp**](https://msdn.microsoft.com/library/aa392389)

[Stampinf](stampinf.md)

[WPP プリプロセッサ](wpp-preprocessor.md)

 

 






