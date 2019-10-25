---
title: ストリームの同期
description: ストリームの同期
ms.assetid: bbf589f1-ca4b-41a2-970d-b31c7761eb1a
keywords:
- 同期 WDK DVD デコーダー
- ストリーム同期 WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6fe3fb69b427285af2672f22feb8f29b45af2b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837673"
---
# <a name="stream-synchronization"></a>ストリームの同期





DVD ストリーム入力は、2つ以上のストリームで構成される場合があります。 Stream クラスドライバーは、DVD デコーダーミニドライバーの代わりに、同期を透過的に処理できます。 詳細については、「[ミニドライバー Synchronization](minidriver-synchronization.md)」を参照してください。 プログラマは、次のような DVD ストリームに影響するいくつかの要因について認識している必要があります。

-   オーディオストリームは、マスタークロックを提供する必要があります。データがない場合は、クロックを合成する必要があります。 オーディオデータが停止すると、オーディオストリームは、 [**Kequeryperformancecounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kequeryperformancecounter)によって返されたレート照合とクロック周波数に基づいてシステムクロックを使用します。 他のすべてのストリームは、オーディオの下位図形として機能する必要があります。 つまり、パフォーマンスをオーディオストリームに同期します。

-   ソフトウェアオーディオデコーダーは、ユーザーモードでサポートされている必要があります。 時計フォワーダー DirectShow フィルターは、ミニドライバーに DirectShow クロックを転送します。 これは、ミニドライバーに対して透過的です。

-   デコーダーでは、プライマリ基本ストリーム (PES) ヘッダーのタイムスタンプを使用しないでください。

-   同期では、システムクロック参照 (SCRs) は使用されません。 Microsoft の DVD アーキテクチャではオーディオとビデオの同期に "マスタークロック" パラダイムが使用されるため、DVD パックの [SCR] フィールドは0に設定されています。

-   ミニドライバーでは、タイムスタンプの不連続性は表示されません。 DVD ナビゲーター/スプリッターを使用すると、すべてのタイムスタンプが連続して作成されます。

デコーダーがオーディオとビデオの両方にデコード機能を提供している場合、デコーダーは、オーディオストリームがシステムのマスタークロックとして開かれている場合にのみ、ハードウェアの同期を使用することができます。 オーディオストリームがマスタークロックでない場合、ビデオストリームはビデオデコードをストリームクラスのマスタークロックに同期する必要があります。

 

 




