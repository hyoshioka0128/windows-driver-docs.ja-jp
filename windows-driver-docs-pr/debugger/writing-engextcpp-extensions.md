---
title: EngExtCpp 拡張機能の作成
description: EngExtCpp 拡張機能の作成
ms.assetid: ac8684f9-26a3-415f-9d96-938ebda29a27
keywords:
- EngExtCpp 拡張機能の記述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0afc5ef5c44130258a540645b65d5033817dabf9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379885"
---
# <a name="writing-engextcpp-extensions"></a>EngExtCpp 拡張機能の作成


## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>


EngExtCpp の拡張機能ライブラリには、標準の C++ コードを含めることができます。 Engextcpp.h と dbgeng.h ヘッダー ファイルの C 関数 wdbgexts.h ヘッダー ファイルに表示されるだけでなくに表示される C++ インターフェイス型を含めることもできます。 Dbgeng.h と wdbgexts.h の両方 engextcpp.h から含まれます。

拡張機能コマンドで使用できる dbgeng.h でインターフェイスの一覧については、次を参照してください。[デバッガー エンジンのリファレンス](https://msdn.microsoft.com/library/windows/hardware/ff540540)します。

拡張機能コマンドで使用できる wdbgexts.h 内の関数の一覧については、次を参照してください。 [WdbgExts 関数](https://msdn.microsoft.com/library/windows/hardware/ff561258)します。 32 ビット版と 64 ビット バージョンにこれらの関数の数が表示されます。 通常、「64」32 ビット バージョンで 64 ビット版の終了があるない数値終了--など**ReadIoSpace64**と**ReadIoSpace**します。 DbgEng 拡張機能から wdbgexts.h 関数を呼び出すときに、常に関数名の拡張子が「64」を使用する必要があります。 これは、ため、[デバッガー エンジン](introduction.md#debugger-engine)64 ビットのポインターは、ターゲット プラットフォームに関係なく内部的には、常に使用します。 Wdbgexts.h を含む、engextcpp.h は API の 64 ビット バージョンを選択します。 **ExtensionApis** WDbgExts API によって使用されるグローバル変数が自動的に EngExtCpp メソッドへのエントリに初期化され、終了時に消去します。

リモートの DbgEng インターフェイスを持つ EngExtCpp 拡張機能を使用する場合、WDbgExts インターフェイスが使用できなくなります、 **ExtensionApis**構造体をゼロに設定することができます。 EngExtCpp 拡張機能のような環境で機能が予想される場合は、WDbgExts API を使用して、避ける必要があります。

**注**  デバッガー拡張機能から、DbgHelp または ImageHlp ルーチンを呼び出そうとする必要があります。 これらのルーチンを呼び出すことはサポートされていませんし、さまざまな問題が発生する可能性があります。

 

 

 





