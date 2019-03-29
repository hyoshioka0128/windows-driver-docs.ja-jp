---
title: スレッドおよび同期の 0 レベル
description: スレッドおよび同期の 0 レベル
ms.assetid: 2baf91e8-fafb-40e2-a24c-cbf04fe45274
keywords:
- WDK の表示、レベル 0 個のスレッド処理
- WDK の表示、0 レベルの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf129424c33ab2073cc23cf1babe220e4e15167e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570943"
---
# <a name="threading-and-synchronization-zero-level"></a>スレッドおよび同期の 0 レベル


Windows 表示 Driver Model (WDDM) は、再入可能な方法で作成する、ディスプレイのミニポート ドライバーを次の呼び出しを許可します。 複数のスレッドでは、次の関数を呼び出すことによって、ドライバーは入力できます同時に。

**注**   2 つのスレッドが 1 つのプロセスに属することができますが、2 つまたは複数のスレッドは、ドライバーで同時に実行できます、します。

 

-   [*DxgkDdiCloseAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559592)

-   [*DxgkDdiCollectDbgInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559595)
    **注**  [*DxgkDdiCollectDbgInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559595)のさまざまなデバッグ情報を収集する必要がありますエラーと高の IRQL でいつでも呼び出すことができます (は、IRQL を*DxgkDdiCollectDbgInfo*で実行されますが一般に未定義)。 いずれの場合も、 *DxgkDdiCollectDbgInfo*適切な同期の必要なデバッグ情報の可用性を確認する必要があります。 ただし場合、**理由**のメンバー、 [ **DXGKARG\_COLLECTDBGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff557545)構造体、 *pCollectDbgInfo*パラメーターの*DxgkDdiCollectDbgInfo*へのポインターに設定されている[ビデオ\_TDR\_タイムアウト\_検出](https://msdn.microsoft.com/library/windows/hardware/hh994433)または[ビデオ\_エンジン\_タイムアウト\_検出](https://msdn.microsoft.com/library/windows/hardware/hh994433)、ドライバーを確認する必要がありますを*DxgkDdiCollectDbgInfo*ページング可能なは、IRQL で実行 =**パッシブ\_レベル**同期 0 レベルをサポートしています。

     

-   [*DxgkDdiControlEtwLogging*](https://msdn.microsoft.com/library/windows/hardware/ff559599)

-   [*DxgkDdiCreateAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559606)

-   [*DxgkDdiCreateContext*](https://msdn.microsoft.com/library/windows/hardware/ff559612)

-   [*DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)

-   [*DxgkDdiDescribeAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559620)

-   [*DxgkDdiDestroyAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559630)

-   [*DxgkDdiDestroyContext*](https://msdn.microsoft.com/library/windows/hardware/ff559636)

-   [*DxgkDdiDestroyDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559639)

-   [*DxgkDdiDpcRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559645)

-   [*DxgkDdiEnumVidPnCofuncModality*](https://msdn.microsoft.com/library/windows/hardware/ff559649)

-   [*DxgkDdiGetScanLine*](https://msdn.microsoft.com/library/windows/hardware/ff559668)

-   [*DxgkDdiGetStandardAllocationDriverData*](https://msdn.microsoft.com/library/windows/hardware/ff559673)

-   [*DxgkDdiInterruptRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559680)

-   [*DxgkDdiIsSupportedVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559684)

-   [*DxgkDdiMiracastCreateContext*](https://msdn.microsoft.com/library/windows/hardware/dn323748)

-   [*DxgkDdiMiracastDestroyContext*](https://msdn.microsoft.com/library/windows/hardware/dn323749)

-   [*DxgkDdiMiracastIoControl*](https://msdn.microsoft.com/library/windows/hardware/dn323750)

-   [*DxgkDdiMiracastQueryCaps*](https://msdn.microsoft.com/library/windows/hardware/dn323751)

-   [*DxgkDdiOpenAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559699)

-   [*DxgkDdiPresent*](https://msdn.microsoft.com/library/windows/hardware/ff559743)

-   [*DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)

-   [*DxgkDdiQueryCurrentFence*](https://msdn.microsoft.com/library/windows/hardware/ff559758)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559775)

-   [*DxgkDdiRecommendVidPnTopology*](https://msdn.microsoft.com/library/windows/hardware/ff559782)

-   [*DxgkDdiRender*](https://msdn.microsoft.com/library/windows/hardware/ff559793)

-   [*DxgkDdiRenderKm*](https://msdn.microsoft.com/library/windows/hardware/ff559800)

-   [*DxgkDdiResetDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559808)

 

 





