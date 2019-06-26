---
title: ミニフィルターの登録解除
description: ミニフィルターの登録解除
ms.assetid: 4af2d4fd-bfbe-4a75-bbfb-2a1c4b5c2032
keywords:
- ミニフィルターの登録を解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fdd8c739aa48c0e7b62d85ac54e4d7c71b4dc0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380315"
---
# <a name="unregistering-the-minifilter"></a>ミニフィルターの登録解除


## <span id="ddk_unregistering_the_minifilter_if"></span><span id="DDK_UNREGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンを呼び出す必要があります[ **FltUnregisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunregisterfilter)ミニフィルター ドライバーの登録を解除するには. 呼び出す**FltUnregisterFilter**により、次の処理を実行します。

-   ミニフィルター ドライバーのコールバック ルーチンは、登録済みでがありません。

-   ミニフィルター ドライバーのインスタンスが破損し、ミニフィルター ドライバーの[ **InstanceTeardownStartCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)と**InstanceTeardownCompleteCallback**ルーチンミニフィルター ドライバーのインスタンスごとと呼ばれます。

-   ミニフィルター ドライバーでは、ボリューム、インスタンス、ストリーム、またはストリームのハンドルは、コンテキストを設定、これらのコンテキストは削除されます。 ミニフィルター ドライバーに登録されている場合、 [**ある CleanupContext は**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)フィルター マネージャーは、指定したコンテキスト タイプのコールバック ルーチン、*ある CleanupContext は*する前に日常的なコンテキストを削除しています。

ミニフィルター ドライバーのフィルターの非透過のポインターでランダウンの未解決の参照がある場合**FltUnregisterFilter**削除されるまで待機状態になります。 ランダウンの未解決の参照が発生するは、通常はミニフィルター ドライバーが呼び出されるため[ **FltQueueGenericWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuegenericworkitem)をシステムの作業キューに作業項目と作業項目を挿入するされていません。キューから削除され、処理します。 (フィルター マネージャー ミニフィルター ドライバーを呼び出すとランダウンの参照を追加します**FltQueueGenericWorkItem**されミニフィルター ドライバーの日常的な取得を操作するときに削除されます)。

ミニフィルター ドライバーはミニフィルター ドライバーのフィルターの非透過のポインターへの参照をランダウンなどの追加する任意のルーチンを呼び出すとランダウンの未解決の参照にも発生[ **FltObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltobjectreference)または[ **FltGetFilterFromInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilterfrominstance)、した後の呼び出しが[ **FltObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltobjectdereference)します。

 

 




