---
title: デバッガーデータモデル-FileSystem 名前空間
description: FileSystem 名前空間には、ファイルシステムを操作するためのプロパティとメソッドが用意されています。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: f5695b2cb62766a0f0444c419ecf644b84e82dc4
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235338"
---
# <a name="the-filesystem-namespace"></a>FileSystem 名前空間

> [!IMPORTANT]
>  このインターフェイスは、アクティブな開発中であり、変更されます。
>
## <a name="summary"></a>まとめ
FileSystem 名前空間には、ファイルシステムを操作するためのプロパティとメソッドが用意されています。 これは、デバッガー拡張機能をサポートするために必要なファイルの読み取りまたは書き込みのために JavaScript から使用できます。

## <a name="sample"></a>サンプル
この名前空間とこれらのオブジェクトを使用する方法の簡単なエンドツーエンドの例については、GitHub のサンプルをご覧ください。https://github.com/Microsoft/WinDbg-Samples/tree/master/FileSystem 

## <a name="object-methods"></a>オブジェクト メソッド
|名前|戻り値の型|署名|説明|
|--- |--- |--- |--- |
|CreateFile|[拡張子](dbgmodel-object-file.md)|CreateFile (パス、[廃棄])|指定したパスに新しいファイルを作成し、書き込み用に開きます。 *ディスポジション*には、"OpenExisting"、"CreateNew"、"createalways" のいずれかを指定できます。|
|CreateTempFile|[拡張子](dbgmodel-object-file.md)|CreateTempFile()|新しい一時ファイルを% TEMP% フォルダーに作成し、書き込み用に開きます。|
|CreateTextReader|[テキストリーダー](dbgmodel-object-text-reader.md)|CreateTextReader (ファイル \| パス、[エンコード])|指定されたエンコーディングのテキストを読み取る、指定された[ファイル](dbgmodel-object-file.md)オブジェクトまたはパスからテキストリーダーを作成します。 エンコードには、"Ascii"、"Utf8"、"Utf16" のいずれかを指定できます。 指定しない場合は、"Ascii" が既定値になります。|
|CreateTextWriter|[テキスト ライター](dbgmodel-object-text-writer.md)|CreateTextWriter (ファイル \| パス、[エンコード])|指定された[ファイル](dbgmodel-object-file.md)オブジェクトまたはパスから、指定したエンコーディングのテキストを書き込むテキストライターを作成します。 エンコードには、"Ascii"、"Utf8"、"Utf16" のいずれかを指定できます。 指定しない場合は、"Ascii" が既定値になります。|
|DeleteFile||DeleteFile (パス)|指定したパスにあるファイルを削除します。|
|FileExists|True または False|FileExists (path)|指定されたパスにファイルが存在するかどうかを示す true または false を返します。|
|OpenFile|[拡張子](dbgmodel-object-file.md)|OpenFile (パス)|読み取り用に指定されたパスにあるファイルを開きます。|

## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|CurrentDirectory|デバッガープロセスの現在の作業ディレクトリを表す[ディレクトリ](dbgmodel-object-directory.md)オブジェクト。|
|Agent.tempdirectory|デバッガープロセスの% TEMP% ディレクトリを表す[ディレクトリ](dbgmodel-object-directory.md)オブジェクト。 |