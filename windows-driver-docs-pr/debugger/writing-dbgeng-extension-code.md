---
title: DbgEng 拡張機能コードの記述
description: このセクションでは、DbgEng の記述について説明します拡張機能のコード
ms.assetid: b1ee686b-986e-46eb-a4bf-93e2de6d1aeb
keywords:
- DbgEng 拡張機能の記述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4936a6b6284daff51b251cb9a8123beadab94dd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530917"
---
# <a name="writing-dbgeng-extension-code"></a>DbgEng 拡張機能コードの記述


## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>


[拡張機能の DbgEng](debugger-engine-and-extension-apis.md)コマンドは、標準の C++ コードを含めることができます。 C 関数 wdbgexts.h ヘッダー ファイルに表示されるだけでなく、dbgeng.h のヘッダー ファイルに表示される C++ インターフェイスも含めることができます。

KDEXT を定義する必要があります wdbgexts.h から関数を使用する場合は、\_wdbgexts.h が含まれる前に、64 ビット。 次に、例を示します。

```cpp
#define KDEXT_64BIT 
#include wdbgexts.h 
#include dbgeng.h 
```

拡張機能コマンドで使用できる dbgeng.h でインターフェイスの一覧については、[デバッガー エンジンのリファレンス](https://msdn.microsoft.com/library/windows/hardware/ff540540)を参照してください。

拡張機能コマンドで使用できる wdbgexts.h 内の関数の一覧については、[WdbgExts 関数](https://msdn.microsoft.com/library/windows/hardware/ff561258)を参照してください。 32 ビット版と 64 ビット バージョンにこれらの関数の数が表示されます。 通常、「64」32 ビット バージョンで 64 ビット版の終了があるない数値終了--など**ReadIoSpace64**と**ReadIoSpace**します。 DbgEng 拡張機能から wdbgexts.h 関数を呼び出すときに、常に関数名の拡張子が「64」を使用する必要があります。 これは、ため、[デバッガー エンジン](introduction.md#debugger-engine)64 ビットのポインターは、ターゲット プラットフォームに関係なく内部的には、常に使用します。

呼び出す必要があります wdbgexts.h を DbgEng 拡張機能に含める場合[ **GetWindbgExtensionApis64** ](https://msdn.microsoft.com/library/windows/hardware/ff549510)拡張 DLL の初期化中に (を参照してください[ *DebugExtensionInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff540476))。

**注**  デバッガー拡張機能から、DbgHelp または ImageHlp ルーチンを呼び出そうとする必要があります。 これらのルーチンを呼び出すことはサポートされていませんし、さまざまな問題が発生する可能性があります。

 

 

 





