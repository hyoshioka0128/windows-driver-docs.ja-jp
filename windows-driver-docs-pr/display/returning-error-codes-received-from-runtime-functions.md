---
title: ランタイム関数から受信したエラー コードを返す
description: ランタイム関数から受信したエラー コードを返す
ms.assetid: 4a2384e8-407f-4248-8b31-7c4e836b15dc
keywords:
- ユーザー モード ドライバー WDK Windows Vista では、ランタイム関数のエラー コードの表示します。
- ランタイム関数のエラー コードの WDK 表示
- エラー コードの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78d51b3e29379bbd75134e7187356fe6da04c6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365635"
---
# <a name="returning-error-codes-received-from-runtime-functions"></a>ランタイム関数から受信したエラー コードを返す


呼び出し、 [Direct3D バージョン 9 ユーザー モード ドライバーによって提供される関数を表示する](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)の呼び出し時に受け取ったエラー コードを返す必要があります、 [Direct3D ランタイムが指定したカーネル サービス関数へのアクセス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index). たとえば、ランタイム呼び出すことができますユーザー モードのディスプレイ ドライバー関数など、 [ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数。 これは、さらなどの呼び出しランタイムによって提供される関数では、 [ **pfnAllocateCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)リソースのメモリを割り当てられません。 ここで、特定の操作を実行する関数。 ランタイムが指定した関数の呼び出しからユーザー モードのディスプレイ ドライバーがエラー コードを受け取ると場合、は、そのエラー コードをランタイムに戻さ返します。

**注**  ドライバーがランタイムに戻さランタイムのエラー コードを渡す必要があるルールに 1 つの例外が発生します。 ドライバーを呼び出すと、 [ **pfnAllocateCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)ビデオ メモリが既に割り当てられているときに、省略可能なリソースのビデオ メモリを割り当て、ランタイムによって提供される関数の規則は適用されません。 場合**pfnAllocateCb**のみ、ドライバーのパフォーマンスを最適化するために必要なオプションのリソースをこのビデオ メモリを割り当ての失敗はメモリ不足のエラーを報告する必要があります (E\_OUTOFMEMORY) ランタイムに戻さします。

 

 

 





