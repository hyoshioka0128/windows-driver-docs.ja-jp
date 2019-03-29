---
title: アダプター コンテキスト フィールドを追跡するための __sdv_save_adapter_context の使用
description: アダプター コンテキスト フィールドを追跡するための __sdv_save_adapter_context の使用
ms.assetid: b43d7ef5-0464-4e07-a5ec-9d7d8a55479e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05980287e270604da7d57d9eab5e8cdbbf8a1a7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579840"
---
# <a name="using-sdvsaveadaptercontext-to-track-adapter-context-fields"></a>使用して\_ \_sdv\_保存\_アダプター\_トラック アダプター コンテキスト フィールドにコンテキスト


NDIS のミニポート ドライバーの呼び出したときに*MiniportInitializeEx*ミニポート アダプター、ドライバーを初期化するためにコールバック関数がミニポート アダプターを表す独自の内部データ構造を作成します。 ドライバーと呼ばれるこの構造体を使用して、*ミニポート アダプター コンテキスト*ミニポート アダプターを管理するために、ドライバーに必要なデバイス固有の状態情報を維持するためにします。 ドライバーは、NDIS この構造体へのハンドルを渡します。

NDIS を呼び出すのミニポート ドライバーのいずれかと*MiniportXxx* NDIS ドライバーに正しいミニポート アダプターを識別するために、ミニポート アダプターのコンテキストを渡す、ミニポート アダプターに関連する関数。 ミニポート アダプタのコンテキストが所有し、ミニポート ドライバーによって保持されるが NDIS してプロトコル ドライバーに不透明であるとします。

ミニポート アダプタのコンテキストでは、NDIS 呼び出しの間、ミニポート ドライバーの状態を保持、するため、Static Driver Verifier (SDV) は、この構造体へのポインターを識別できる必要があります。 SDV ミニポート ドライバーの状態を追跡を有効にする必要がありますに保存するハンドル ミニポート アダプタのコンテキストを使用して、  **\_ \_sdv\_保存\_アダプター\_コンテキスト**関数。

 **\_ \_Sdv\_保存\_アダプター\_コンテキスト**関数には、次の構文。

```
__sdv_save_adapter_context( &adapter_context ) 
```

場所アダプター\_コンテキストは、ミニポート ドライバーで定義されているミニポート アダプタのコンテキストを識別するハンドル。 この関数は、ミニポート ドライバーのコンテキストで 1 回だけ呼び出す必要があります。

 **\_ \_Sdv\_保存\_アダプター\_コンテキスト**関数は静的分析ツールでのみ使用されます。 この関数は、コンパイラによって無視されます。

次のコード例に示しますを呼び出すタイミング\_ \_sdv\_保存\_アダプター\_コンテキストと SDV での情報を追跡する方法、*ミニポート アダプター コンテキスト*します。

次のコード例は、ミニポート アダプター コンテキスト サンプル構造 MP の簡略化されたバージョンを示しています。\_アダプター。

```
typedef struct _MP_ADAPTER
{
    NDIS_HANDLE             AdapterHandle;

    BOOLEAN                 InterruptRegistered;
    NDIS_HANDLE             InterruptHandle;

    /* ..................... */

} MP_ADAPTER, *PMP_ADAPTER;
```

実行中に*MiniportInitializeEx*、MP 用のメモリ\_アダプターの構造が割り当てられます。 メモリの割り当ての直後に続く **\_ \_sdv\_保存\_アダプター\_コンテキスト**が呼び出されます。

呼び出す必要があります、  **\_ \_sdv\_保存\_アダプター\_コンテキスト**ミニポート アダプタのコンテキストの構造体への有効なポインターがあると、すぐに機能します。

```
NDIS_STATUS 
MPInitialize(
    IN  NDIS_HANDLE                        MiniportAdapterHandle,
    IN  NDIS_HANDLE                        MiniportDriverContext,
    IN  PNDIS_MINIPORT_INIT_PARAMETERS     MiniportInitParameters
    )
{
    NDIS_STATUS     Status = NDIS_STATUS_SUCCESS;
    PMP_ADAPTER     pAdapter = NULL;
 
    /* ..................... */
 
    do
    {
   // allocate the memory for the AdapterContext
        pAdapter = NdisAllocateMemoryWithTagPriority(
            MiniportAdapterHandle,
            sizeof(MP_ADAPTER),
            NIC_TAG,
            LowPoolPriority
            );

   // save the adapter context, even before we check whether it is NULL or not 
 __sdv_save_adapter_context(&pAdapter);

        if (pAdapter == NULL)
        {
            Status = NDIS_STATUS_RESOURCES;
            break;
        }
 
        NdisZeroMemory(pAdapter, sizeof(MP_ADAPTER));
 
        pAdapter->AdapterHandle = MiniportAdapterHandle;
        pAdapter->PauseState = NicPaused;

   /* ..................... */
```

次のコード例では、SDV ミニポート アダプタのコンテキスト内の値を追跡する方法を示します。 この例で、ドライバーは、ミニポートで提供される関数を呼び出すことによって、割り込みを登録します*MpRegisterInterrupt*します。 ミニポート アダプタのコンテキストにドライバーが、結果を保存、呼び出しが成功した場合 (*pAdapter*) フィールド、InterruptRegistered します。

```
//
// Register the interrupt
   //
        Status = MpRegisterInterrupt(pAdapter);
        if (Status != NDIS_STATUS_SUCCESS)
        {
            break;
        }
 
   // save the value of the result into the AdapterContext
        pAdapter->InterruptRegistered = TRUE;
```

NDIS ミニポート ドライバーは、中止するのには、呼び出し、ドライバーの*MiniportHaltEx*ミニポート アダプタのコンテキストにハンドルを渡すことによって機能します。 SDV は、以前の呼び出しから、このハンドルもあるので **\_ \_sdv\_保存\_アダプター\_コンテキスト**、SDV InterruptRegistered フィールドの値を追跡できます。

```
VOID MPHalt(
    IN  NDIS_HANDLE             MiniportAdapterContext,
    IN  NDIS_HALT_ACTION        HaltAction
    )
{
    PMP_ADAPTER     pAdapter = (PMP_ADAPTER) MiniportAdapterContext;
 
    /* ..................... */

    if (pAdapter->InterruptRegistered)
    {
        NdisMDeregisterInterruptEx(pAdapter->InterruptHandle);
        pAdapter->InterruptRegistered = FALSE;
    }

/* ..................... */
```

 

 





