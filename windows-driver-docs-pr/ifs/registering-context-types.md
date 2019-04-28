---
title: コンテキストの種類の登録
description: コンテキストの種類の登録
ms.assetid: ddf03426-5c49-4621-b81d-59d1cb002ae9
keywords:
- 型の登録、コンテキスト WDK ファイル システム ミニフィルター
- コンテキストの種類を登録します。
- FLT_CONTEXT_REGISTRATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 242c3363cdcb79f479bd13360ad623be53b57740
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370110"
---
# <a name="registering-context-types"></a>コンテキストの種類の登録


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーを呼び出すと[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)からその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンをする必要があります登録する必要が各型のコンテキストを使用します。

ミニフィルター ドライバーをコンテキストの種類を登録するには、可変長配列を作成します[ **FLT\_コンテキスト\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544629)構造体し、配列へのポインターを格納します**ContextRegistration**のメンバー、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)でミニフィルター ドライバーに合格する構造体、 *登録*パラメーターの[ **FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)します。 この配列内の要素の順序は重要ではありません。 ただし、配列内の最後の要素があります {0} FLT\_コンテキスト\_終了しました。

ミニフィルター ドライバーを使用するコンテキスト種類ごとにする必要があります指定する必要が少なくとも 1 つのコンテキストの定義に、FLT の形式で\_コンテキスト\_登録構造体。 各 FLT\_コンテキスト\_登録構造型、サイズ、およびその他のコンテキスト情報を定義します。

ミニフィルター ドライバーが呼び出すことによって新しいコンテキストを作成するときに[ **FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)、フィルター マネージャーを使用して、*サイズ*のパラメーター、 **FltAllocateContext**ルーチン、だけでなく**サイズ**と**フラグ**、FLT のメンバー\_コンテキスト\_登録構造を選択しますコンテキストの定義に使用します。

固定サイズのコンテキストの**サイズ**、FLT のメンバー\_コンテキスト\_登録構造 (ミニフィルター ドライバーで定義されているコンテキストの構造体の部分のバイト単位)、サイズを指定します。 コンテキストの最大サイズは、MAXUSHORT (64 KB) です。 0 は、有効なサイズ値です。 フィルター マネージャーは、ルック アサイド リストを使用して固定サイズのコンテキストを実装します。 フィルター マネージャーが 2 つのルック アサイド リストの各サイズの値を作成します。 1 つのページと 1 つの非ページ。

可変サイズのコンテキストの**サイズ**FLT にメンバーを設定する必要があります\_変数\_サイズ\_コンテキスト。 フィルター マネージャーは、ページまたは非ページ プールから直接、可変サイズのコンテキストを割り当てます。

**フラグ**、FLT のメンバー\_コンテキスト\_登録構造、FLTFL\_コンテキスト\_登録\_いいえ\_EXACT\_サイズ\_のマッチ フラグを指定することができます。 ミニフィルター ドライバーは固定サイズのコンテキストを使用すると、このフラグが指定されて、フィルター マネージャーは、コンテキストのサイズが要求されたサイズ以上である場合、ルック アサイド リストからコンテキストを割り当てます。 それ以外の場合、コンテキストのサイズは、要求されたサイズと同じである必要があります。

ミニフィルター ドライバーには、特定のコンテキスト型の場合、それぞれに別のサイズ、最大 3 つ固定サイズのコンテキストの定義と変数サイズの 1 つの定義を指定できます。 詳細については、次を参照してください。 [ **FLT\_コンテキスト\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544629)します。

ミニフィルター ドライバーは、必要に応じて、コンテキストが解放される前に呼び出されるコンテキスト クリーンアップ コールバック ルーチンを指定できます。 詳細については、次を参照してください。 [ **PFLT\_コンテキスト\_クリーンアップ\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551078)します。

ミニフィルター ドライバーでは、これらのタスクを実行するフィルター マネージャーではなく、コンテキストを解放したり、独自のコールバック ルーチンを必要に応じて定義できます。 ただし、この非常にまれに必要です。 詳細については、次を参照してください[ **PFLT\_コンテキスト\_ALLOCATE\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551075)と[ **PFLT\_コンテキスト。\_無料\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551082)します。

ミニフィルター ドライバーの CTX サンプルから取得されますが、次のコード例は、FLT の配列を示しています。\_コンテキスト\_インスタンス、ファイル、ストリーム、およびファイル オブジェクト (ストリームのハンドル) のコンテキストを登録するために使用する構造体を登録します。

```cpp
const FLT_CONTEXT_REGISTRATION contextRegistration[] =
{
    { FLT_INSTANCE_CONTEXT,              //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_INSTANCE_CONTEXT_SIZE,         //Size
      CTX_INSTANCE_CONTEXT_TAG           //PoolTag
    },
    { FLT_FILE_CONTEXT,                  //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_FILE_CONTEXT_SIZE,             //Size
      CTX_FILE_CONTEXT_TAG               //PoolTag
    },
    { FLT_STREAM_CONTEXT,                //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_STREAM_CONTEXT_SIZE,           //Size
      CTX_STREAM_CONTEXT_TAG             //PoolTag
    },
    { FLT_STREAMHANDLE_CONTEXT,          //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_STREAMHANDLE_CONTEXT_SIZE,     //Size
      CTX_STREAMHANDLE_CONTEXT_TAG       //PoolTag
    },
    { FLT_CONTEXT_END }
};
```

 

 




