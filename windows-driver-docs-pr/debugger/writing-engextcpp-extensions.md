---
title: EngExtCpp 拡張機能の作成
description: EngExtCpp 拡張機能の作成
ms.assetid: ac8684f9-26a3-415f-9d96-938ebda29a27
keywords:
- EngExtCpp 拡張機能、書き込み
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78b99c8deb3e5960f65cb2a2f66e13c3d43e47e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534255"
---
# <a name="writing-engextcpp-extensions"></a>EngExtCpp 拡張機能の作成


## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>


EngExtCpp 拡張ライブラリには、任意の標準 C++ コードを含めることができます。 また、engextcpp ヘッダーファイルと dbgeng .h ヘッダーファイルに表示される C++ インターフェイスや、wdbgexts ヘッダーファイルに表示される C 関数を含めることもできます。 Engextcpp には、dbgeng. h と wdbgexts の両方が含まれています。

拡張コマンドで使用できる dbgeng. h のインターフェイスの完全な一覧については、「[デバッガーエンジンリファレンス](debugger-engine-reference.md)」を参照してください。

拡張コマンドで使用できる wdbgexts .h の関数の完全な一覧については、「 [Wdbgexts 関数](wdbgexts-functions.md)」を参照してください。 これらの関数の多くは、32ビットバージョンと64ビットバージョンで表示されます。 通常、64ビットバージョンは "64" で終わり、32ビットバージョンには数値の終わりがありません (たとえば、 **ReadIoSpace64**と**ReadIoSpace**)。 DbgEng 拡張機能から wdbgexts. h 関数を呼び出すときは、必ず "64" で終わる関数名を使用する必要があります。 これは、ターゲットプラットフォームに関係なく、[デバッガーエンジン](introduction.md#debugger-engine)が常に64ビットポインターを内部的に使用するためです。 Wdbgexts. h を含めると、engextcpp は64ビットバージョンの API を選択します。 WDbgExts API によって使用される**extensionapis**グローバル変数は、EngExtCpp メソッドにエントリで自動的に初期化され、終了時に消去されます。

リモートの DbgEng インターフェイスで EngExtCpp 拡張機能を使用すると、WDbgExts インターフェイスを使用できなくなり、 **Extensionapis**構造体をゼロにすることができます。 EngExtCpp 拡張機能がこのような環境で機能することが予想される場合は、WDbgExts API の使用を避ける必要があります。

**メモ**   どのデバッガー拡張機能からでも、DbgHelp または Imagehlp.dll ルーチンを呼び出すことはできません。 これらのルーチンの呼び出しはサポートされていないため、さまざまな問題が発生する可能性があります。

 

 

 





