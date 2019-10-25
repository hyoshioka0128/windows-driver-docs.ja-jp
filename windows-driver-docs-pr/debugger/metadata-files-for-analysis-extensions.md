---
title: 分析拡張機能プラグインのメタデータ ファイル
description: また、分析拡張機能のプラグインを記述するときに、プラグインを呼び出す必要がある状況を記述するメタデータファイルも記述します。
ms.assetid: 13B9B7A5-1D68-49A3-825B-454AC070FCC1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36ccae904dae8756c6ca058ec463b0a279c571d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834344"
---
# <a name="metadata-files-for-analysis-extension-plug-ins"></a>分析拡張機能プラグインのメタデータ ファイル


また、分析拡張機能のプラグインを記述するときに、プラグインを呼び出す必要がある状況を記述するメタデータファイルも記述します。 [ **! Analyze**](-analyze.md)デバッガーコマンドを実行すると、メタデータファイルを使用して、読み込むプラグインを特定します。

Analysis extension プラグインと同じ名前で、拡張子が alz のメタデータファイルを作成します。 たとえば、分析拡張機能のプラグインの名前が MyAnalyzer .dll の場合、メタデータファイルは MyAnalyzer. alz という名前にする必要があります。 分析拡張機能プラグインと同じディレクトリにメタデータファイルを配置します。

分析拡張機能プラグインのメタデータファイルは、キーと値のペアを含む ASCII テキストファイルです。 キーと値は空白で区切られます。 キーには、空白以外の文字を含めることができます。 キーの大文字と小文字は区別されません。

キーと次の空白文字の後に、対応する値が開始されます。 値には、次のいずれかの形式を使用できます。

-   行の末尾の任意の文字セット。 このフォームは、改行文字が含まれていない値に対して機能します。

    **重要**  メタデータファイルの最後の値にこの形式の値が含まれている場合、行の終わりには改行文字を使用する必要があります。

     

-   中かっこ {} の間の任意の文字セット。 フォームは、改行文字を含む値に対して機能します。

\# で始まる行はコメントであるため、無視されます。 コメントは、キーが必要な場合にのみ開始できます。

メタデータファイルでは、次のキーを使用できます。

| Key            | 説明                                                                                                                                                                                                                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PluginId       | 文字列-プラグインを識別します。                                                                                                                                                                                                                                                                  |
| DebuggeeClass  | 文字列-有効な値は "Kernel" と "User" です。 プラグインがカーネルモードのエラーのみを分析するか、ユーザーモードのエラーのみを分析することを目的としていることを示します。                                                                                                                                     |
| バグチェックコード   | 32ビットバグチェックコード-プラグインがこの[バグチェックコード](bug-check-code-reference2.md)を分析することに関心があることを示します。 1つのメタデータファイルで複数のバグチェックコードを指定できます。                                                                                                  |
| ExceptionCode  | 32ビット例外コード-プラグインがこの[例外コード](https://go.microsoft.com/fwlink/p?LinkID=282670)を分析することに関心があることを示します。 1つのメタデータファイルで複数の例外コードを指定できます。                                                                                 |
| ExecutableName | 文字列-このプラグインが、分析対象のプロセスの実行中の実行可能ファイルであるセッションだけを対象とすることを示します。 1つのメタデータファイルで、複数の実行可能ファイル名を指定できます。                                                                                              |
| ImageName      | 文字列-既定の分析では、このイメージ (dll、sys、または exe) がエラーになっていると見なされる場合にのみ、プラグインが関心を持つことを示します。 プラグインは、エラーが発生しているイメージを分析した後に呼び出されます。 1つのメタデータファイルで複数のイメージ名を指定できます。 |
| MaxTagCount    | Integer-プラグインが必要とするカスタムタグの最大数。 カスタムタグは、extsfns で定義されているもの以外のタグです。                                                                                                                                                                |

 

## <a name="span-idexample_metadata_filesspanspan-idexample_metadata_filesspanspan-idexample_metadata_filesspanexample-metadata-files"></a><span id="Example_Metadata_Files"></span><span id="example_metadata_files"></span><span id="EXAMPLE_METADATA_FILES"></span>メタデータファイルの例


次のメタデータファイルは、バグチェックコード0xE2 の分析に関係するプラグインを記述しています。 (最後の行は改行文字で終わる必要があることを思い出してください)。

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0xE2
```

次のメタデータファイルは、エラーの発生時に MyDriver がモジュールであると見なされた場合のバグチェック0x8、0x9、および0xA の分析に関心のあるプラグインを記述します。

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0x8
BugCheckCode  0x9
BugCheckCode  0xA
ImageName     MyDriver.sys
```

次のメタデータファイルは、MyApp が分析対象のプロセスの実行可能ファイルである場合に、例外コード0xC0000005 の分析に関心のあるプラグインを記述します。 また、プラグインによって、最大3つのカスタムタグが作成される場合もあります。

```text
PluginId        MyPlugin
DebuggeeClass   User
ExceptionCode   0xC0000005
ExecutableName  MyApp.exe
```

Windows 用デバッグツールには、dbgexts という名前のデバッガー拡張モジュールを構築するために使用できるサンプルが用意されています。 この拡張モジュールはいくつかのデバッガー拡張機能のコマンドを実装しますが、analysis extension プラグインとしても機能します。つまり、 [ **\_EFN\_Analyze**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)関数がエクスポートされます。 次に示すのは、分析拡張機能のプラグインとして dbgexts dll を記述するメタデータファイルです。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[拡張用の分析拡張機能プラグインを記述しています。](writing-an-analysis-extension-to-extend--analyze.md)

[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)

[ **! 分析**](-analyze.md)

 

 






