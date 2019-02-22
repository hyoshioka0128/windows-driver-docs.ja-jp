---
title: ミニフィルターの登録を解除
description: ミニフィルターの登録を解除
ms.assetid: 4af2d4fd-bfbe-4a75-bbfb-2a1c4b5c2032
keywords:
- ミニフィルターの登録を解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f324979ab0975083aeabbf78b227bee33f23446
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549718"
---
# <a name="unregistering-the-minifilter"></a>ミニフィルターの登録を解除


## <span id="ddk_unregistering_the_minifilter_if"></span><span id="DDK_UNREGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)ルーチンを呼び出す必要があります[ **FltUnregisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544606)ミニフィルター ドライバーの登録を解除するには. 呼び出す**FltUnregisterFilter**により、次の処理を実行します。

-   ミニフィルター ドライバーのコールバック ルーチンは、登録済みでがありません。

-   ミニフィルター ドライバーのインスタンスが破損し、ミニフィルター ドライバーの[ **InstanceTeardownStartCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551098)と**InstanceTeardownCompleteCallback**ルーチンミニフィルター ドライバーのインスタンスごとと呼ばれます。

-   ミニフィルター ドライバーでは、ボリューム、インスタンス、ストリーム、またはストリームのハンドルは、コンテキストを設定、これらのコンテキストは削除されます。 ミニフィルター ドライバーに登録されている場合、 [**ある CleanupContext は**](https://msdn.microsoft.com/library/windows/hardware/ff551078)フィルター マネージャーは、指定したコンテキスト タイプのコールバック ルーチン、*ある CleanupContext は*する前に日常的なコンテキストを削除しています。

ミニフィルター ドライバーのフィルターの非透過のポインターでランダウンの未解決の参照がある場合**FltUnregisterFilter**削除されるまで待機状態になります。 ランダウンの未解決の参照が発生するは、通常はミニフィルター ドライバーが呼び出されるため[ **FltQueueGenericWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff543452)をシステムの作業キューに作業項目と作業項目を挿入するされていません。キューから削除され、処理します。 (フィルター マネージャー ミニフィルター ドライバーを呼び出すとランダウンの参照を追加します**FltQueueGenericWorkItem**されミニフィルター ドライバーの日常的な取得を操作するときに削除されます)。

ミニフィルター ドライバーはミニフィルター ドライバーのフィルターの非透過のポインターへの参照をランダウンなどの追加する任意のルーチンを呼び出すとランダウンの未解決の参照にも発生[ **FltObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff543382)または[ **FltGetFilterFromInstance**](https://msdn.microsoft.com/library/windows/hardware/ff543049)、した後の呼び出しが[ **FltObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff543378)します。

 

 




