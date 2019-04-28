---
title: WdbgExts 拡張機能コードの作成
description: WdbgExts 拡張機能コードの作成
ms.assetid: bb37ea19-8355-42f3-aca5-32cc2b3be3b2
keywords:
- WdbgExts 拡張機能
- 拡張機能、WdbgExts
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e895a8a9305905ec60e3b790bc62539e05e75b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374800"
---
# <a name="writing-wdbgexts-extension-code"></a>WdbgExts 拡張機能コードの作成


## <span id="ddk_writing_wdbgexts_extension_code_dbwx"></span><span id="DDK_WRITING_WDBGEXTS_EXTENSION_CODE_DBWX"></span>


WdbgExts 拡張機能コマンドでは、WdbgExts.h ヘッダー ファイルに表示されるデバッガー関連の関数だけでなく、すべて標準の C 関数を呼び出すことができます。

WdbgExts 関数は、デバッガーの拡張機能コマンドのみで使用を対象としています。 これらは、制御して、コンピューターまたはデバッグ中にアプリケーションを調べることに役立ちます。 これらの WdbgExts 関数を呼び出しているコードによって WdbgExts.h ヘッダー ファイルを含める必要があります。

これらの関数の数は、32 ビット版と 64 ビット バージョンがあります。 「64、」で、64 ビットの WdbgExts 関数の名前を一般に、末尾たとえば**ReadIoSpace64**します。 32 ビット バージョンがあるない数値終了では、たとえば、 **ReadIoSpace**します。 64 ビット ポインターを使用している場合は、関数名の拡張子が「64」; を使用する必要があります。32 ビット ポインターを使用している場合は、「装飾されていない」の関数名を使用する必要があります。 作成することの任意の拡張機能の 64 ビット ポインターが推奨されます。 参照してください[32 ビット ポインターと 64 ビット ポインター](32-bit-pointers-and-64-bit-pointers.md)詳細についてはします。

WdbgExts 拡張機能は、DbgEng.h ヘッダー ファイルで表示される C++ インターフェイスを使用できません。 これらのインターフェイスを使用する場合は、する必要がありますまたは作成する DbgEng 拡張子 EngExtCpp 拡張機能代わりにします。 DbgEng.h 内のすべてのインターフェイスおよび WdbgExts.h で DbgEng 拡張機能と EngExtCpp 拡張機能の両方で使用できます。 詳細については、次を参照してください。 [DbgEng 拡張機能の作成](writing-dbgeng-extensions.md)と[EngExtCpp 拡張機能の作成](writing-engextcpp-extensions.md)です。

**注**  デバッガー拡張機能から、DbgHelp または ImageHlp ルーチンを呼び出そうとする必要があります。 これはサポートされていませんし、さまざまな問題が発生する可能性があります。

 

次のトピックでは、WdbgExts 関数のさまざまなカテゴリの概要を説明します。

[WdbgExts 入力と出力](wdbgexts-input-and-output.md)

[WdbgExts メモリへのアクセス](wdbgexts-memory-access.md)

[WdbgExts スレッドとプロセス](wdbgexts-threads-and-processes.md)

[WdbgExts シンボル](wdbgexts-symbols.md)

[WdbgExts ターゲットの情報](wdbgexts-target-information.md)

これらの関数の一覧については、次を参照してください。 [WdbgExts 関数](https://msdn.microsoft.com/library/windows/hardware/ff561258)します。

 

 





