---
title: 拡張機能と拡張機能関数の呼び出し
description: 拡張機能と拡張機能関数の呼び出し
ms.assetid: 0582cdc2-7059-42db-878b-28767a6fe850
keywords:
- デバッガーエンジン API、呼び出し (拡張機能を)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: daa6f04e85c275a779b876ca01242b4c2f5519a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837831"
---
# <a name="calling-extensions-and-extension-functions"></a>拡張機能と拡張機能関数の呼び出し


拡張ライブラリを読み込む (または既に読み込まれている拡張ライブラリのハンドルを取得する) には、 [**Addextension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-addextension)を使用します。 拡張ライブラリは、 [**Removeextension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removeextension)を使用してアンロードできます。

拡張コマンドは、 [**callextension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-callextension)を使用して呼び出すことができます。

### <a name="span-idextension_functionsspanspan-idextension_functionsspanextension-functions"></a><span id="extension_functions"></span><span id="EXTENSION_FUNCTIONS"></span>拡張関数

*拡張関数*は、拡張ライブラリによってエクスポートされる関数です。 これらは任意の関数プロトタイプを使用でき、C 関数ポインターを使用して直接呼び出されます。

これらは拡張コマンドではなく、デバッガーコマンドでは使用できません。 拡張関数をリモートで呼び出すことはできません。これらは直接呼び出す必要があります。 そのため、これらをクライアントのデバッグから使用することはできません。 クライアントオブジェクトがホストエンジン内にある場合にのみ呼び出すことができます。リモートでデバッグしない場合、またはスマートクライアントを使用している場合にのみ呼び出すことができます。

拡張機能は、拡張ライブラリ内で、名前の前に "\_EFN\_" を付加して識別されます。

拡張関数へのポインターを取得するには、 [**Getextensionfunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getextensionfunction)を使用します。 この関数ポインターの型は、拡張関数のプロトタイプと一致している必要があります。 拡張関数は、C の他の関数ポインターと同じように呼び出すことができるようになりました。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

次の拡張関数が拡張ライブラリに含まれており、デバッガーエンジンに読み込まれている場合は、次のようになります。

```cpp
HRESULT CALLBACK
_EFN_GetObject(IDebugClient * client, SomeObject * obj);
```

次のものを使用して呼び出すことができます。

```cpp
typedef ULONG (CALLBACK * GET_OBJECT)(IDebugClient * client, SomeObject * obj);



HRESULT status = S_OK;
GET_OBJECT extFn = NULL;
SomeObject myObj;

if (g_DebugControl->
        GetExtensionFunction(0,
                             "GetObject",
                             (FARPROC *) &extFn ) == S_OK &&
    extFn)
{
    status = (*extFn)(client, &myObj);
}
```

 

 





