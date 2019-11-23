---
title: コンテキストの種類の登録
description: コンテキストの種類の登録
ms.assetid: ddf03426-5c49-4621-b81d-59d1cb002ae9
keywords:
- コンテキスト WDK ファイルシステムミニフィルター, 型の登録
- コンテキスト型の登録
- FLT_CONTEXT_REGISTRATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce7c9956228b33f55e7d1cdc5ccdd334e819c907
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841008"
---
# <a name="registering-context-types"></a>コンテキストの種類の登録


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルタードライバーが[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)を呼び出すと、使用する各種類のコンテキストを登録する必要があります。

コンテキスト型を登録するために、ミニパスドライバーは、 [**FLT\_コンテキスト\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_context_registration)構造体の可変長配列を作成し、その配列へのポインターを、ミニフィルタードライバーが[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)の*登録*パラメーターに渡す[**FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体の**contextregistration**メンバーに格納します。 この配列内の要素の順序は関係ありません。 ただし、配列の最後の要素は {FLT\_CONTEXT\_END} である必要があります。

ミニフィルタードライバーが使用するコンテキストの種類ごとに、FLT\_コンテキスト\_登録構造の形式でコンテキスト定義を少なくとも1つ指定する必要があります。 各 FLT\_コンテキスト\_の登録構造は、コンテキストの型、サイズ、およびその他の情報を定義します。

ミニフィルタードライバーで[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)を呼び出すことによって新しいコンテキストを作成する場合、フィルターマネージャー**は FltAllocateContext**ルーチンの*size*パラメーターと、FLT\_Context\_REGISTRATION 構造体の**size**および**Flags**メンバーを使用して、使用するコンテキスト定義を選択します。

固定サイズのコンテキストの場合、FLT\_コンテキスト\_の登録構造の**サイズ**メンバーは、ミニフィルタードライバーによって定義されるコンテキスト構造の一部のサイズをバイト単位で指定します。 コンテキストの最大サイズは MAXUSHORT (64 KB) です。 0は有効なサイズ値です。 フィルターマネージャーは、ルックアサイドリストを使用して固定サイズのコンテキストを実装します。 フィルターマネージャーは、各サイズ値に対して2つのルックアサイドリストを作成します。1つはページングされていて、もう1つはページ

可変サイズのコンテキストの場合は、 **size**メンバーを FLT に設定する必要があります。\_変数\_サイズ\_コンテキストに設定します。 フィルターマネージャーは、ページングされたプールまたは非ページプールから、可変サイズのコンテキストを直接割り当てます。

FLT\_CONTEXT\_REGISTRATION 構造体の**Flags**メンバーでは、FLTFL\_コンテキスト\_登録\_\_完全\_サイズ\_一致フラグを指定することはできません。 ミニフィルタードライバーで固定サイズのコンテキストが使用されていて、このフラグが指定されている場合、コンテキストのサイズが要求されたサイズ以上の場合、フィルターマネージャーはルックアサイドリストからコンテキストを割り当てます。 それ以外の場合は、コンテキストのサイズが要求されたサイズと同じである必要があります。

指定されたコンテキストの種類では、ミニフィルタードライバーは最大3つの固定サイズのコンテキスト定義を指定できます。それぞれ異なるサイズを持ち、1つの可変サイズの定義があります。 詳細については、「 [**FLT\_CONTEXT\_REGISTRATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_context_registration)」を参照してください。

ミニフィルタードライバーでは、コンテキストが解放される前に呼び出されるコンテキストクリーンアップコールバックルーチンをオプションで指定できます。 詳細については、「 [**PFLT\_CONTEXT\_CLEANUP\_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)」を参照してください。

ミニフィルタードライバーでは、必要に応じて、フィルターマネージャーに依存してこれらのタスクを実行するのではなく、コンテキストを割り当てて解放するための独自のコールバックルーチンを定義できます。 ただし、これはほとんど必要ありません。 詳細については、「 [**PFLT\_context\_ALLOCATE\_callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_allocate_callback) 」と「 [**PFLT\_CONTEXT\_FREE\_callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_free_callback)」を参照してください。

CTX サンプルミニフィルタードライバーから取得された次のコード例では、インスタンス、ファイル、ストリーム、およびファイルオブジェクト (ストリームハンドル) のコンテキストを登録するために使用される、FLT\_コンテキスト\_登録構造の配列が示されています。

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

 

 




