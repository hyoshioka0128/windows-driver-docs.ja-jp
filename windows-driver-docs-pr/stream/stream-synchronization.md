---
title: ストリームの同期
description: ストリームの同期
ms.assetid: bbf589f1-ca4b-41a2-970d-b31c7761eb1a
keywords:
- 同期の WDK DVD デコーダー
- ストリームの同期の WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 770c5eb6fdadff569192a6d88c0d1d28d275a5d5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377782"
---
# <a name="stream-synchronization"></a>ストリームの同期





DVD のストリーム入力の 2 つまたは複数のストリームで構成されます。 ストリーム クラス ドライバーは、DVD デコーダーのミニドライバー代わり透過的に同期を処理できます。 詳細については、次を参照してください。[ミニドライバー同期](minidriver-synchronization.md)します。 プログラマはなど、DVD のストリームに影響を与えるいくつかの要因を意識する必要があります。

-   オーディオ ストリームは、マスターのクロックを提供する必要があり、データがない場合、クロックを合成する必要があります。 オーディオ ストリームがによって返される速度に一致して、クロック周波数に基づいて、システム クロックを使用するオーディオ データが停止したら、 [ **KeQueryPerformanceCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kequeryperformancecounter)します。 他のすべてのストリームは、オーディオを下位として機能する必要があります。 つまり、オーディオ ストリームへのパフォーマンスを同期します。

-   オーディオのソフトウェア デコーダーは、ユーザー モードでサポートする必要があります。 クロックのフォワーダー DirectShow フィルターは、ミニドライバーに DirectShow クロックを転送します。 これは、ミニドライバーに透過的です。

-   デコーダーは、プライマリ基本ストリーム (PES) ヘッダーのタイムスタンプを使用しないでください。

-   システム クロックの参照 (SCRs) は、同期では使用されません。 DVD パックの SCR フィールドは、Microsoft の DVD のアーキテクチャでは、「マスター クロック」パラダイムを使用して、オーディオとビデオの同期するためにゼロに設定されます。

-   ミニドライバーは、タイム スタンプの不連続性を認識しません。 DVD のナビゲーター/分割では、すべてのタイムスタンプが隣接します。

デコーダーは、オーディオとビデオの両方のデコード機能を提供する場合、デコーダーは、マスター システム クロックとオーディオのストリームを開いたときだけハードウェアの同期を使用できます。 オーディオ ストリームがマスターのクロックでない場合、ビデオ ストリームがストリーム クラスのマスター クロックにビデオ デコーディングを同期する必要があります。

 

 




