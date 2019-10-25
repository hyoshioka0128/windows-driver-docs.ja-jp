---
title: フィルターモジュールのデタッチ
description: フィルターモジュールのデタッチ
ms.assetid: ef987f2f-a681-4ddb-959a-1becdf633678
keywords:
- フィルターモジュール WDK ネットワーク、デタッチ
- フィルターモジュールのデタッチ
- フィルタードライバーの WDK ネットワーク, フィルターモジュールのデタッチ
- NDIS フィルタードライバー (WDK)、フィルターモジュールのデタッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22474dfcd4c89f420dc9762fecee0f10938e1960
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838153"
---
# <a name="detaching-a-filter-module"></a>フィルターモジュールのデタッチ





ドライバースタックからフィルターモジュールをデタッチするプロセスを開始するために、NDIS はフィルタードライバーの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出します。 *Filterdetach*関数での実行の開始時に、フィルターモジュールは*デタッチ*された状態に入ります。 フィルターモジュールをデタッチする前に、NDIS はドライバースタックを一時停止する必要があります。 ドライバースタックの一時停止の詳細については、「[ドライバースタックの一時停止](pausing-a-driver-stack.md)」を参照してください。

*Filterdetach*関数では、ドライバーは、影響を受けるフィルターモジュールのコンテキスト領域とその他のリソース (バッファープールなど) を解放します。 フィルタードライバーが*Filterdetach*への呼び出しに失敗することはできません。 したがって、アタッチ操作中に、デタッチ操作を正常に実行するために必要なすべてのリソースが、フィルタードライバーによって事前に割り当てられる必要があります。 フィルターモジュールのアタッチの詳細については、「[フィルターモジュールのアタッチ](attaching-a-filter-module.md)」を参照してください。

フィルターモジュールが*Filterdetach*から戻ると、NDIS は一時停止されたドライバースタックを開始できます。 ドライバースタックを開始する方法の詳細については、「[ドライバースタックを開始する](starting-a-driver-stack.md)」を参照してください。

 

 





