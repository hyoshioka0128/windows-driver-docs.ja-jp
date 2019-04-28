---
title: デバッガーのデータ モデル - FileSystem Namespace
description: ファイル システム名前空間は、ファイル システムを操作するためのメソッドとプロパティを提供します。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: d73b2b61c9846aaadcafe089b5d98fe7d8371812
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374922"
---
> [!IMPORTANT]
>  このインターフェイスは開発と、変更されます。
>
# <a name="the-filesystem-namespace"></a>FileSystem Namespace
## <a name="summary"></a>概要
ファイル システム名前空間は、ファイル システムを操作するためのメソッドとプロパティを提供します。 これは、JavaScript からの読み取りまたは書き込み、デバッガーの拡張機能をサポートするために必要なファイルを使用できます。

## <a name="sample"></a>サンプル
これを使用する方法の簡単なエンド ツー エンド例の名前空間と、これらのオブジェクトをチェック アウト - GitHub のサンプル https://github.com/Microsoft/WinDbg-Samples/tree/master/FileSystem 

## <a name="object-methods"></a>オブジェクトのメソッド
|名前|戻り値の型|署名|説明|
|--- |--- |--- |--- |
|CreateFile|[file](dbgmodel-object-file.md)|CreateFile (パス、[破棄])|指定したパスに新しいファイルを作成し、書き込み用に開きます。 *廃棄*"OpenExisting"、"CreateNew"または"CreateAlways"のいずれかを指定することがあります。|
|CreateTempFile|[file](dbgmodel-object-file.md)|CreateTempFile()|%TEMP% フォルダーに新しい一時ファイルを作成し、書き込み用に開きます。|
|CreateTextReader|[テキスト リーダー](dbgmodel-object-text-reader.md)|CreateTextReader(file \| path, [encoding])|テキスト リーダーを作成、特定[ファイル](dbgmodel-object-file.md)オブジェクトまたはパスが指定したエンコーディングのテキストを読み取る。 エンコーディングと、"Ascii"、"Utf8"または"Utf16"のいずれかのことがあります。 指定しない場合、既定値は、"Ascii"。|
|CreateTextWriter|[テキスト ライター](dbgmodel-object-text-writer.md)|CreateTextWriter(file \| path, [encoding])|テキスト ライターを作成する、指定された[ファイル](dbgmodel-object-file.md)オブジェクトまたは指定したエンコーディングのテキストを記述するパス。 エンコーディングと、"Ascii"、"Utf8"または"Utf16"のいずれかのことがあります。 指定しない場合、既定値は、"Ascii"。|
|DeleteFile||DeleteFile(path)|指定したパスにファイルを削除します。|
|FileExists|True または False|FileExists(path)|True または false、ファイルが指定されたパスに存在するかどうかを返します。|
|OpenFile|[file](dbgmodel-object-file.md)|OpenFile(path)|読み取り用に指定されたパスにファイルを開きます。|

## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|CurrentDirectory|A[ディレクトリ](dbgmodel-object-directory.md)デバッガー プロセスの現在の作業ディレクトリを表すオブジェクト。|
|TempDirectory|A[ディレクトリ](dbgmodel-object-directory.md)デバッガー プロセスの %TEMP% ディレクトリを表すオブジェクト。 |