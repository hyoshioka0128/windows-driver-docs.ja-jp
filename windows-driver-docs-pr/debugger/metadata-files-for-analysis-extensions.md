---
title: 分析拡張機能プラグインのメタデータ ファイル
description: プラグイン分析拡張機能を記述するときに、呼び出されるプラグイン状況について説明しますメタデータ ファイルを作成します。
ms.assetid: 13B9B7A5-1D68-49A3-825B-454AC070FCC1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1544f26c71207c0e25d294ee2d8b1d645cd999a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366474"
---
# <a name="metadata-files-for-analysis-extension-plug-ins"></a>分析拡張機能プラグインのメタデータ ファイル


プラグイン分析拡張機能を記述するときに、呼び出されるプラグイン状況について説明しますメタデータ ファイルを作成します。 ときに、 [ **! 分析**](-analyze.md)デバッガー コマンドが実行され、メタデータ ファイルを使ってロード プラグインを決定します。

プラグイン分析拡張機能と .alz の拡張機能と同じ名前を持つメタデータ ファイルを作成します。 たとえば、MyAnalyzer.dll プラグイン分析拡張機能の名前が場合、メタデータ ファイルする必要があります指定 MyAnalyzer.alz。 プラグイン、分析の拡張機能と同じディレクトリにメタデータ ファイルを配置します。

プラグイン分析拡張機能のメタデータ ファイルは、キーと値のペアを含む ASCII テキスト ファイルです。 キーと値は空白で区切られます。 キーは、任意の非空白文字を持つことができます。 キーは大文字小文字が区別されません。

キー、次の空白文字と、対応する値を開始します。 値は、次の形式のいずれかができます。

-   行の末尾に文字のセット。 このフォームは、改行文字を含まない値に対して機能します。

    **重要な**  メタデータ ファイルの最後の値は、このフォームの値を持つ場合に、改行文字行末する必要があります。

     

-   間に中かっこ {} を任意の文字セット。 フォームは、改行文字が含まれている値に対して機能します。

始まる行\#はコメントでは無視されます。 コメントは、キーが必要な場合のみ開始できます。

メタデータ ファイルでは、次のキーを使用できます。

| Key            | 説明                                                                                                                                                                                                                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| プラグイン Id       | 文字列 - プラグインを識別します。                                                                                                                                                                                                                                                                  |
| DebuggeeClass  | 文字列の値は、"Kernel"または"User"です。 のみカーネル モードの障害やユーザー モードのエラーのみを分析でプラグインが関心があることを示します。                                                                                                                                     |
| BugCheckCode   | 32 ビットのバグ チェックのコードでは、この分析で、プラグインが関心があることを示します[チェックのコードをバグ](bug-check-code-reference2.md)します。 単一のメタデータ ファイルには、複数のバグ チェック コードを指定できます。                                                                                                  |
| ExceptionCode  | 32 ビットの例外コードのことを示す、プラグインがこの分析[例外コード](https://go.microsoft.com/fwlink/p?LinkID=282670)します。 単一のメタデータ ファイルには、複数の例外コードを指定できます。                                                                                 |
| ExecutableName | 文字列 - セッションでのみ、プラグインが関心があることを示します。 これは、分析するプロセスの実行可能ファイルの場所。 単一のメタデータ ファイルには、複数の実行可能ファイル名を指定できます。                                                                                              |
| ImageName      | 文字列 - プラグインのみ興味を示している既定の分析が (dll、sys、または exe) が原因の場合に、このイメージを考慮するセッションでのみを示します。 分析が障害があるどのイメージを決定した後、このプラグインが呼び出されます。 単一のメタデータ ファイルには、複数のイメージ名を指定できます。 |
| MaxTagCount    | 整数の最大数のカスタム タグがニーズをプラグインします。 カスタム タグは、extsfns.h で定義されているもの以外のタグです。                                                                                                                                                                |

 

## <a name="span-idexamplemetadatafilesspanspan-idexamplemetadatafilesspanspan-idexamplemetadatafilesspanexample-metadata-files"></a><span id="Example_Metadata_Files"></span><span id="example_metadata_files"></span><span id="EXAMPLE_METADATA_FILES"></span>メタデータ ファイルの例


次のメタデータ ファイルはバグ チェック コード 0 xe2 を分析することに関心がプラグインについて説明します。 (取り消し、最後の行は、改行文字で終わる必要があります)。

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0xE2
```

次のメタデータ ファイルが MyDriver.sys はエラー時のモジュールと見なされる場合、0x8、0x9、および 0 xa のバグ チェックの分析に関心がある場合はプラグインについて説明します。

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0x8
BugCheckCode  0x9
BugCheckCode  0xA
ImageName     MyDriver.sys
```

次のメタデータ ファイルが MyApp.exe が解析中のプロセスの実行可能ファイルの場合は、例外コード 0xC0000005 を分析に関心がプラグインについて説明します。 また、プラグインが 3 台のカスタム タグを作成します。

```text
PluginId        MyPlugin
DebuggeeClass   User
ExceptionCode   0xC0000005
ExecutableName  MyApp.exe
```

ビルドに使用できるサンプルにはデバッグ ツールの Windows dbgexts.dll をという名前のデバッガー拡張機能モジュール。 この拡張機能モジュールがいくつかのデバッガー拡張機能のコマンドを実装することも提供することが分析の拡張機能としてプラグインです。つまり、エクスポート、 [  **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)関数。 プラグインの分析拡張機能として dbgexts.dll を記述するメタデータ ファイルを次に示します。

```text
PluginId         PluginSample
DebuggeeClass   User
ExceptionCode   0xc0000005
ExecutableName      cdb.exe
ExecutableName      windbg.exe
#
# Custom tag descriptions 
#
TagDesc         0xA0000000  SAMPLE_PLUGIN_DEBUG_TEXT    {Sample debug
help text from plug-in analysis}
#
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[分析の拡張機能プラグインを拡張する記述! 分析](writing-an-analysis-extension-to-extend--analyze.md)

[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)

[ **! 分析**](-analyze.md)

 

 






