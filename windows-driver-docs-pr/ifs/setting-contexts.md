---
title: コンテキストの設定
description: コンテキストの設定
ms.assetid: 3daa23e6-14d7-4d35-8bc8-695296cd289d
keywords:
- 設定、コンテキスト WDK ファイル システム ミニフィルター
- コンテキストのアタッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f14427def7d85c90985442f48f3ff8b81218c5ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582259"
---
# <a name="setting-contexts"></a>コンテキストの設定


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


新しいコンテキストを作成すると、ミニフィルター ドライバーに接続できるオブジェクトを呼び出して**FltSet***Xxx***コンテキスト**ここで、 *Xxx*コンテキスト型です。

場合、*操作*のパラメーター、 **FltSet***Xxx***コンテキスト**ルーチンが FLT に設定されている\_設定\_コンテキスト\_KEEP\_場合\_EXISTS、 **FltSet***Xxx***コンテキスト**ミニフィルター ドライバーでオブジェクトのコンテキストが既に設定されていない場合にのみ、新しく割り当てられたコンテキストをオブジェクトにアタッチします。 ミニフィルター ドライバーには、コンテキストは既に設定する場合**FltSet***Xxx***コンテキスト**ステータスを返します\_FLT\_コンテキスト\_ALREADY\_は定義済みNTSTATUS エラー コード、および既存のコンテキストは置き換えられません。 場合、 *OldContext*のパラメーター、 **FltSet***Xxx***コンテキスト**ルーチンが非**NULL**、既存のコンテキストへのポインターを受け取ります。 このポインターは必要がなくなったら、ミニフィルター ドライバー解放する必要があります、呼び出すことによって[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)します。

場合、*操作*FLT にパラメーターが設定されている\_設定\_コンテキスト\_置換\_場合\_EXISTS、 **FltSet***Xxx***コンテキスト**オブジェクトに新しいコンテキストを常にアタッチします。 ミニフィルター ドライバーには、コンテキストは既に設定する場合**FltSet***Xxx***コンテキスト**既存のコンテキストを削除しますを新しいコンテキストを設定し、新しいコンテキストの参照カウントをインクリメントします。 場合、 *OldContext*パラメーターは非**NULL**、削除されたコンテキストへのポインターを受け取ります。 このポインターは必要がなくなったら、ミニフィルター ドライバー解放する必要があります、呼び出すことによって**FltReleaseContext**します。

CTX サンプルのミニフィルター ドライバーから取得した次のコード例で、 **CtxInstanceSetup**ルーチンを作成し、インスタンス コンテキストを設定します。

```cpp
status = FltAllocateContext(
           FltObjects->Filter,           //Filter
           FLT_INSTANCE_CONTEXT,         //ContextType
           CTX_INSTANCE_CONTEXT_SIZE,    //ContextSize
           NonPagedPool,                 //PoolType
           &instanceContext);            //ReturnedContext
...
status = FltSetInstanceContext(
           FltObjects->Instance,              //Instance
           FLT_SET_CONTEXT_KEEP_IF_EXISTS,    //Operation
           instanceContext,                   //NewContext
           NULL);                             //OldContext

if (instanceContext != NULL) {
  FltReleaseContext(instanceContext);
}
return status;
```

呼び出し後[ **FltSetInstanceContext**](https://msdn.microsoft.com/library/windows/hardware/ff544521)への呼び出しがある**FltReleaseContext**によって設定された参照カウントを解放する[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710) (*いない* **FltSetInstanceContext**)。 これについては説明[解放コンテキスト](releasing-contexts.md)します。

 

 




