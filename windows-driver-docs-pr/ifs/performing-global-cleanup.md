---
title: グローバル クリーンアップの実行
description: グローバル クリーンアップの実行
ms.assetid: 18e0fca0-16ec-4ca9-8b71-47f58f41c46d
keywords:
- グローバル クリーンアップ WDK ファイル システム ミニフィルター
- クリーンアップ WDK ファイル システム ミニフィルター グローバル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a45d0ddf5b51cf153ca8706d7fd02c2887f1c2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385159"
---
# <a name="performing-global-cleanup"></a>グローバル クリーンアップの実行


## <span id="ddk_performing_global_cleanup_if"></span><span id="DDK_PERFORMING_GLOBAL_CLEANUP_IF"></span>


ミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンが必要なグローバル クリーンアップを実行する必要があります。 ミニフィルター ドライバーが実行する可能性がグローバルのクリーンアップ タスクの例を以下に示します。

-   呼び出す[ **ExDeleteResourceLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)以前の呼び出しによって初期化されたグローバル リソース変数を削除する[ **ExInitializeResourceLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite).

-   呼び出す[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)または[ **ExFreePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag) などのルーチンへの前回の呼び出しで割り当てられたグローバルメモリを解放するには[**Exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)します。

-   呼び出す[ **ExDeleteNPagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist)または[ **ExDeletePagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist)で割り当てられたルック アサイド リストを削除する、以前の呼び出し[ **ExInitializeNPagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)または[ **ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)、それぞれします。

-   呼び出す[ **PsRemoveCreateThreadNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psremovecreatethreadnotifyroutine)または[ **PsRemoveLoadImageNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psremoveloadimagenotifyroutine)グローバル コールバック ルーチンの登録を解除するには以前の呼び出しによって登録されたを[ **PsSetCreateThreadNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)または[ **PsSetLoadImageNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetloadimagenotifyroutine)、それぞれします。

 

 




