---
title: グローバル クリーンアップの実行
description: グローバル クリーンアップの実行
ms.assetid: 18e0fca0-16ec-4ca9-8b71-47f58f41c46d
keywords:
- グローバル クリーンアップ WDK ファイル システム ミニフィルター
- クリーンアップ WDK ファイル システム ミニフィルター グローバル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d6420a1275a74761c329237354664b3c38de7e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352860"
---
# <a name="performing-global-cleanup"></a>グローバル クリーンアップの実行


## <span id="ddk_performing_global_cleanup_if"></span><span id="DDK_PERFORMING_GLOBAL_CLEANUP_IF"></span>


ミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)ルーチンが必要なグローバル クリーンアップを実行する必要があります。 ミニフィルター ドライバーが実行する可能性がグローバルのクリーンアップ タスクの例を以下に示します。

-   呼び出す[ **ExDeleteResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544578)以前の呼び出しによって初期化されたグローバル リソース変数を削除する[ **ExInitializeResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545317).

-   呼び出す[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)または[ **ExFreePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544593) などのルーチンへの前回の呼び出しで割り当てられたグローバルメモリを解放するには[**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)します。

-   呼び出す[ **ExDeleteNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff544566)または[ **ExDeletePagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff544570)で割り当てられたルック アサイド リストを削除する、以前の呼び出し[ **ExInitializeNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545301)または[ **ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)、それぞれします。

-   呼び出す[ **PsRemoveCreateThreadNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559947)または[ **PsRemoveLoadImageNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559949)グローバル コールバック ルーチンの登録を解除するには以前の呼び出しによって登録されたを[ **PsSetCreateThreadNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559954)または[ **PsSetLoadImageNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559957)、それぞれします。

 

 




