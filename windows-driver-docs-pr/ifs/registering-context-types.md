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
ms.openlocfilehash: ebf643f312da061a6102562953cf988bbc0aac52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385139"
---
# <a name="registering-context-types"></a>コンテキストの種類の登録


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーを呼び出すと[ **FltRegisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)からその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンをする必要があります登録する必要が各型のコンテキストを使用します。

ミニフィルター ドライバーをコンテキストの種類を登録するには、可変長配列を作成します[ **FLT\_コンテキスト\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_context_registration)構造体し、配列へのポインターを格納します**ContextRegistration**のメンバー、 [ **FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)でミニフィルター ドライバーに合格する構造体、 *登録*パラメーターの[ **FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)します。 この配列内の要素の順序は重要ではありません。 ただし、配列内の最後の要素があります {0} FLT\_コンテキスト\_終了しました。

ミニフィルター ドライバーを使用するコンテキスト種類ごとにする必要があります指定する必要が少なくとも 1 つのコンテキストの定義に、FLT の形式で\_コンテキスト\_登録構造体。 各 FLT\_コンテキスト\_登録構造型、サイズ、およびその他のコンテキスト情報を定義します。

ミニフィルター ドライバーが呼び出すことによって新しいコンテキストを作成するときに[ **FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecontext)、フィルター マネージャーを使用して、*サイズ*のパラメーター、 **FltAllocateContext**ルーチン、だけでなく**サイズ**と**フラグ**、FLT のメンバー\_コンテキスト\_登録構造を選択しますコンテキストの定義に使用します。

固定サイズのコンテキストの**サイズ**、FLT のメンバー\_コンテキスト\_登録構造 (ミニフィルター ドライバーで定義されているコンテキストの構造体の部分のバイト単位)、サイズを指定します。 コンテキストの最大サイズは、MAXUSHORT (64 KB) です。 0 は、有効なサイズ値です。 フィルター マネージャーは、ルック アサイド リストを使用して固定サイズのコンテキストを実装します。 フィルター マネージャーが 2 つのルック アサイド リストの各サイズの値を作成します。 1 つのページと 1 つの非ページ。

可変サイズのコンテキストの**サイズ**FLT にメンバーを設定する必要があります\_変数\_サイズ\_コンテキスト。 フィルター マネージャーは、ページまたは非ページ プールから直接、可変サイズのコンテキストを割り当てます。

**フラグ**、FLT のメンバー\_コンテキスト\_登録構造、FLTFL\_コンテキスト\_登録\_いいえ\_EXACT\_サイズ\_のマッチ フラグを指定することができます。 ミニフィルター ドライバーは固定サイズのコンテキストを使用すると、このフラグが指定されて、フィルター マネージャーは、コンテキストのサイズが要求されたサイズ以上である場合、ルック アサイド リストからコンテキストを割り当てます。 それ以外の場合、コンテキストのサイズは、要求されたサイズと同じである必要があります。

ミニフィルター ドライバーには、特定のコンテキスト型の場合、それぞれに別のサイズ、最大 3 つ固定サイズのコンテキストの定義と変数サイズの 1 つの定義を指定できます。 詳細については、次を参照してください。 [ **FLT\_コンテキスト\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_context_registration)します。

ミニフィルター ドライバーは、必要に応じて、コンテキストが解放される前に呼び出されるコンテキスト クリーンアップ コールバック ルーチンを指定できます。 詳細については、次を参照してください。 [ **PFLT\_コンテキスト\_クリーンアップ\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)します。

ミニフィルター ドライバーでは、これらのタスクを実行するフィルター マネージャーではなく、コンテキストを解放したり、独自のコールバック ルーチンを必要に応じて定義できます。 ただし、この非常にまれに必要です。 詳細については、次を参照してください[ **PFLT\_コンテキスト\_ALLOCATE\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_allocate_callback)と[ **PFLT\_コンテキスト。\_無料\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_free_callback)します。

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

 

 




