---
title: 拡張機能と拡張機能関数の呼び出し
description: 拡張機能と拡張機能関数の呼び出し
ms.assetid: 0582cdc2-7059-42db-878b-28767a6fe850
keywords:
- デバッガー エンジン API、拡張機能を呼び出す
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d13410c18b4fcb259c811f05611a1e370485fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374451"
---
# <a name="calling-extensions-and-extension-functions"></a>拡張機能と拡張機能関数の呼び出し


拡張機能ライブラリを読み込む (または、既に読み込まれた拡張機能ライブラリのハンドルを取得する) を使用して[ **AddExtension**](https://msdn.microsoft.com/library/windows/hardware/ff537892)します。 拡張機能ライブラリをアンロードできるようにする[ **RemoveExtension**](https://msdn.microsoft.com/library/windows/hardware/ff554497)します。

使用して拡張機能のコマンドを呼び出すことができます[ **CallExtension**](https://msdn.microsoft.com/library/windows/hardware/ff539023)します。

### <a name="span-idextensionfunctionsspanspan-idextensionfunctionsspanextension-functions"></a><span id="extension_functions"></span><span id="EXTENSION_FUNCTIONS"></span>拡張関数

*拡張関数*は拡張機能ライブラリによってエクスポートされる関数です。 任意の関数プロトタイプを使用することができますを使用して直接 C 関数ポインターと呼ばれます。

拡張機能のコマンドは、デバッガー コマンドでは利用できません。 拡張関数をリモートから呼び出すことができません。それらを直接呼び出す必要があります。 そのためのクライアントをデバッグから使用できません。 できますのみ呼び出すことがクライアント オブジェクトは、リモートではデバッグ時、またはスマート クライアントを使用する場合、ホストのエンジンの内部でがの場合。

拡張関数が、拡張機能ライブラリ内で識別される、"\_EFN\_"名には、先頭に付加します。

拡張関数へのポインターを取得する[ **GetExtensionFunction**](https://msdn.microsoft.com/library/windows/hardware/ff546733)します。 この関数ポインターの型は、拡張関数のプロトタイプと一致する必要があります。 C 言語で他の関数ポインターと同じように、拡張関数を呼び出すようになりましたことが

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の拡張関数が、拡張機能ライブラリに含まれ、デバッガー エンジンに読み込まれます。

```cpp
HRESULT CALLBACK
_EFN_GetObject(IDebugClient * client, SomeObject * obj);
```

使用して呼び出す可能性があります。

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

 

 





