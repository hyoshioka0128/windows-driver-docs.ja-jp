---
title: DbgEng 拡張機能コードの作成
description: このセクションでは、DbgEng の記述について説明します拡張機能のコード
ms.assetid: b1ee686b-986e-46eb-a4bf-93e2de6d1aeb
keywords:
- DbgEng 拡張機能の記述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41bbdea3bb3257b51ad5fc75edaa3a75b94b620a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369393"
---
# <a name="writing-dbgeng-extension-code"></a>DbgEng 拡張機能コードの作成


## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>


[拡張機能の DbgEng](debugger-engine-and-extension-apis.md)コマンドは、標準の C++ コードを含めることができます。 C 関数 wdbgexts.h ヘッダー ファイルに表示されるだけでなく、dbgeng.h のヘッダー ファイルに表示される C++ インターフェイスも含めることができます。

KDEXT を定義する必要があります wdbgexts.h から関数を使用する場合は、\_wdbgexts.h が含まれる前に、64 ビット。 次に、例を示します。

```cpp
#define KDEXT_64BIT 
#include wdbgexts.h 
#include dbgeng.h 
```

拡張機能コマンドで使用できる dbgeng.h でインターフェイスの一覧については、次を参照してください。[デバッガー エンジンのリファレンス](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-engine-reference)します。

拡張機能コマンドで使用できる wdbgexts.h 内の関数の一覧については、次を参照してください。 [WdbgExts 関数](https://docs.microsoft.com/windows-hardware/drivers/debugger/wdbgexts-functions)します。 32 ビット版と 64 ビット バージョンにこれらの関数の数が表示されます。 通常、「64」32 ビット バージョンで 64 ビット版の終了があるない数値終了--など**ReadIoSpace64**と**ReadIoSpace**します。 DbgEng 拡張機能から wdbgexts.h 関数を呼び出すときに、常に関数名の拡張子が「64」を使用する必要があります。 これは、ため、[デバッガー エンジン](introduction.md#debugger-engine)64 ビットのポインターは、ターゲット プラットフォームに関係なく内部的には、常に使用します。

呼び出す必要があります wdbgexts.h を DbgEng 拡張機能に含める場合[ **GetWindbgExtensionApis64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getwindbgextensionapis64)拡張 DLL の初期化中に (を参照してください[ *DebugExtensionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_initialize))。

**注**  デバッガー拡張機能から、DbgHelp または ImageHlp ルーチンを呼び出そうとする必要があります。 これらのルーチンを呼び出すことはサポートされていませんし、さまざまな問題が発生する可能性があります。

 

 

 





