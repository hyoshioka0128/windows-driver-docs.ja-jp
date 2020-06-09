---
title: DbgEng 拡張機能コードの作成
description: このセクションでは、DbgEng 拡張機能コードの記述について説明します。
ms.assetid: b1ee686b-986e-46eb-a4bf-93e2de6d1aeb
keywords:
- DbgEng 拡張機能、書き込み
ms.date: 10/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2eeb68d94acf7acbf6df8fecb8ccb8a542e9425e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534259"
---
# <a name="writing-dbgeng-extension-code"></a>DbgEng 拡張機能コードの作成

## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>

[Dbgeng 拡張](debugger-engine-and-extension-apis.md)コマンドには、任意の標準 C++ コードを含めることができます。 また、wdbgexts ヘッダーファイルに表示される C 関数に加えて、dbgeng .h ヘッダーファイルに表示される C++ インターフェイスを含めることもできます。

Wdbgexts から関数を使用する場合は、 \_ wdbgexts が含まれる前に KDEXT の64ビットを定義する必要があります。 次に例を示します。

```cpp
#define KDEXT_64BIT
#include wdbgexts.h
#include dbgeng.h
```

拡張コマンドで使用できる dbgeng. h のインターフェイスの完全な一覧については、「[デバッガーエンジンリファレンス](debugger-engine-reference.md)」を参照してください。

拡張コマンドで使用できる wdbgexts .h の関数の完全な一覧については、「 [Wdbgexts 関数](wdbgexts-functions.md)」を参照してください。 これらの関数の多くは、32ビットバージョンと64ビットバージョンで表示されます。 通常、64ビットバージョンは "64" で終わり、32ビットバージョンには数値の終わりがありません (たとえば、 **ReadIoSpace64**と**ReadIoSpace**)。 DbgEng 拡張機能から wdbgexts. h 関数を呼び出すときは、必ず "64" で終わる関数名を使用する必要があります。 これは、ターゲットプラットフォームに関係なく、[デバッガーエンジン](introduction.md#debugger-engine)が常に64ビットポインターを内部的に使用するためです。

DbgEng 拡張機能に wdbgexts を含める場合は、拡張 DLL の初期化中に[**GetWindbgExtensionApis64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getwindbgextensionapis64)を呼び出す必要があります (「 [*debugextensioninitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_initialize)」を参照してください)。

**メモ**   どのデバッガー拡張機能からでも、DbgHelp または Imagehlp.dll ルーチンを呼び出すことはできません。 これらのルーチンの呼び出しはサポートされていないため、さまざまな問題が発生する可能性があります。
