---
title: WdbgExts 拡張機能コードの作成
description: WdbgExts 拡張機能コードの作成
ms.assetid: bb37ea19-8355-42f3-aca5-32cc2b3be3b2
keywords:
- WdbgExts 拡張機能
- 拡張機能、WdbgExts
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf05f04fae4f061528235928e7c1e72829945f1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534243"
---
# <a name="writing-wdbgexts-extension-code"></a>WdbgExts 拡張機能コードの作成


## <span id="ddk_writing_wdbgexts_extension_code_dbwx"></span><span id="DDK_WRITING_WDBGEXTS_EXTENSION_CODE_DBWX"></span>


WdbgExts 拡張機能のコマンドでは、任意の標準 C 関数を呼び出すことができます。また、WdbgExts ヘッダーファイルに表示されるデバッガー関連の関数を呼び出すこともできます。

WdbgExts 関数は、デバッガー拡張機能コマンドでのみ使用することを目的としています。 これらは、デバッグされているコンピューターまたはアプリケーションの制御と検査に役立ちます。 WdbgExts ヘッダーファイルは、これらの WdbgExts 関数を呼び出すコードに含まれている必要があります。

これらの関数には、32ビットバージョンと64ビットバージョンがあります。 通常、64ビットの WdbgExts 関数の名前は、 **ReadIoSpace64**などの "64" で終わります。 32ビットバージョンでは、 **ReadIoSpace**のように、数値の末尾がありません。 64ビットポインターを使用している場合は、"64" で終わる関数名を使用する必要があります。32ビットポインターを使用している場合は、"非装飾" 関数名を使用する必要があります。 64-記述する拡張機能には、ビットポインターを使用することをお勧めします。 詳細については、「 [32 ビットポインター」と「64ビットポインター](32-bit-pointers-and-64-bit-pointers.md) 」を参照してください。

WdbgExts 拡張機能では、DbgEng .h ヘッダーファイルに表示される C++ インターフェイスを使用できません。 これらのインターフェイスを使用する場合は、代わりに DbgEng 拡張機能または EngExtCpp 拡張機能を記述する必要があります。 DbgEng 拡張機能と EngExtCpp 拡張機能の両方で、DbgEng. h 内のすべてのインターフェイスだけでなく、WdbgExts 内のすべてのインターフェイスも使用できます。 詳細については、「 [DbgEng 拡張機能の作成](writing-dbgeng-extensions.md)」および「 [EngExtCpp 拡張機能の記述](writing-engextcpp-extensions.md)」を参照してください。

**メモ**   デバッガー拡張機能から、DbgHelp または Imagehlp.dll のルーチンを呼び出さないでください。 これはサポートされていないため、さまざまな問題が発生する可能性があります。

 

次のトピックでは、WdbgExts 関数のさまざまなカテゴリの概要について説明します。

[WdbgExts の入力と出力](wdbgexts-input-and-output.md)

[WdbgExts のメモリ アクセス](wdbgexts-memory-access.md)

[WdbgExts のスレッドとプロセス](wdbgexts-threads-and-processes.md)

[WdbgExts のシンボル](wdbgexts-symbols.md)

[WdbgExts のターゲット情報](wdbgexts-target-information.md)

これらの関数の完全な一覧については、「 [Wdbgexts 関数](wdbgexts-functions.md)」を参照してください。

 

 





