---
title: コンテキストの作成
description: コンテキストの作成
ms.assetid: da62d79d-064b-4ea4-abed-ffb13a9cc13d
keywords:
- WDK のコンテキストのファイル システム ミニフィルターを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2d6d8bff653c96d1c5d44a41312b8c8224ab1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359370"
---
# <a name="creating-contexts"></a>コンテキストの作成


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


呼び出してコンテキストを作成できるミニフィルター ドライバーが使用されるコンテキストの種類を登録すると、 [ **FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)します。 このルーチンで説明されている条件に従って使用する適切なコンテキストの定義を選択します。[コンテキスト型を登録する](registering-context-types.md)します。

次のコード例で、CTX サンプル ミニフィルター ドライバーから取得した、 **CtxInstanceSetup**ルーチンの呼び出し[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)インスタンス コンテキストを作成するには:

```cpp
status = FltAllocateContext(
 FltObjects->Filter,           //Filter
           FLT_INSTANCE_CONTEXT,         //ContextType
           CTX_INSTANCE_CONTEXT_SIZE,    //ContextSize
 NonPagedPool,                 //PoolType
           &instanceContext);            //ReturnedContext
```

CTX サンプルでは、インスタンス コンテキストのコンテキストの定義を次に登録されます。

```cpp
{ FLT_INSTANCE_CONTEXT,              //ContextType
  0,                                 //Flags
 CtxContextCleanup,                 //ContextCleanupCallback
  CTX_INSTANCE_CONTEXT_SIZE,         //Size
  CTX_INSTANCE_CONTEXT_TAG },        //PoolTag
```

これは、ためにの固定サイズのコンテキストの定義を**サイズ**メンバーは定数です。 (場合、**サイズ**メンバーが FLT\_変数\_サイズ\_コンテキスト、可変サイズのコンテキストの定義をなります)。なお、FLTFL\_コンテキスト\_登録\_いいえ\_EXACT\_サイズ\_一致フラグが設定されていない、**フラグ**メンバー。 この場合は場合の値、*サイズ*パラメーターの[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)のものと一致する、**サイズ**コンテキストのメンバー定義上、 **FltAllocateContext**適切な非ページのルック アサイド リストから、インスタンス コンテキストを割り当てます。 値が一致しない場合**FltAllocateContext**失敗の状態の戻り値を持つ\_FLT\_コンテキスト\_割り当て\_いない\_が見つかりました。

[**FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)いずれかに新しいコンテキストの参照カウントを初期化します。 コンテキストが不要になったとき、ミニフィルター ドライバーは、この参照を解放する必要があります。 したがって、すべての呼び出しに**FltAllocateContext**後続の呼び出しによって照合される必要があります[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)します。

 

 




