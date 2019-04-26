---
title: DECLARE_API Macro の使用
description: DECLARE_API Macro の使用
ms.assetid: 469f5ae4-2da8-4bbe-b5c0-75fcef227ba5
keywords:
- WdbgExts 拡張機能、DECLARE_API マクロ
- DECLARE_API マクロ (WdbgExts)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bef24f2a95008024f023fb1f89fa18f4b8ffffd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340488"
---
# <a name="using-the-declareapi-macro"></a>DECLARE を使用して\_API マクロ


## <span id="ddk_using_the_declare_api_macro_dbwx"></span><span id="DDK_USING_THE_DECLARE_API_MACRO_DBWX"></span>


DECLARE を使用して、WdbgExts 拡張 DLL 内の各拡張機能コマンドが宣言された\_API マクロ。 このマクロは、wdbgexts.h で定義されます。

拡張機能コマンドのコードの基本的な形式です。

```cpp
DECLARE_API( myextension )
{
    code for myextension
}
```

DECLARE\_API マクロが拡張機能コマンドの標準的なインターフェイスを設定します。 などの場合は、ユーザーには、拡張機能のコマンドに引数が渡される、全体の引数文字列が文字列として格納され、この文字列 (PCSTR) へのポインターとして拡張関数に渡される**args**します。

64 ビットのポインター、DECLARE を使用している場合\_API マクロは次のように定義されます。

```cpp
#define DECLARE_API(s)                             \
    CPPMOD VOID                                    \
    s(                                             \
        HANDLE                 hCurrentProcess,    \
        HANDLE                 hCurrentThread,     \
        ULONG64                dwCurrentPc,        \
        ULONG                  dwProcessor,        \
        PCSTR                  args                \
     )
```

32 ビット ポインターの宣言を使用している場合\_API は、点を除いて、同じまま**dwCurrentPc** ULONG64 ではなく ULONG 型になります。 ただし、64 ビット ポインターが任意の拡張機能を推奨、記述すること。 参照してください[32 ビット ポインターと 64 ビット ポインター](32-bit-pointers-and-64-bit-pointers.md)詳細についてはします。

 

 





