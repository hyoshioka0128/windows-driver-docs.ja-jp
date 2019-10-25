---
title: グローバルクリーンアップを実行しています
description: グローバルクリーンアップを実行しています
ms.assetid: 18e0fca0-16ec-4ca9-8b71-47f58f41c46d
keywords:
- グローバルクリーンアップ WDK ファイルシステムミニフィルター
- グローバル WDK ファイルシステムミニフィルターのクリーンアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018a6c77b544c540b5dda7ee437dc9d503164ef2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841033"
---
# <a name="performing-global-cleanup"></a>グローバルクリーンアップを実行しています


## <span id="ddk_performing_global_cleanup_if"></span><span id="DDK_PERFORMING_GLOBAL_CLEANUP_IF"></span>


ミニフィルタードライバーの[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンでは、必要なグローバルクリーンアップを実行する必要があります。 次の一覧に、ミニフィルタードライバーによって実行される可能性のあるグローバルクリーンアップタスクの例を示します。

-   [**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)を呼び出して、以前の[**Ex Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)の呼び出しで初期化されたグローバルリソース変数を削除します。

-   [**Exfreeatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)などのルーチンの前の呼び出しで割り当てられたグローバルメモリを解放するには、 [**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)または[**exfreepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)を呼び出します。

-   [**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)または[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)を呼び出して、 [**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)または[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)の前回の呼び出しで割り当てられたルックアサイドリストを削除します。4.3.

-   [**PsRemoveCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremovecreatethreadnotifyroutine)または[**PsRemoveLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremoveloadimagenotifyroutine)を呼び出して、 [**Pssetcreatethreadnotifyroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)への以前の呼び出しで登録されたグローバルコールバックルーチンの登録を解除します。または[ **、PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutine)。

 

 




