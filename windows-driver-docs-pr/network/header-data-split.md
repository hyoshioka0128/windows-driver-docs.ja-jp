---
title: ヘッダー データの分割
description: ヘッダー データの分割
ms.assetid: ecbf4b08-8be4-42ca-8a65-1cb8124bee33
keywords:
- ヘッダー データは、WDK を分割
- ヘッダーとデータを別のバッファーの分割
- WDK のヘッダー データ バッファーを分割します。
- 受信側のデータの WDK ネットワーク
- WDK のヘッダー データ フレームに分割します。
- フレーム WDK ヘッダー以外のデータの分割を分割します。
- 記憶域 WDK ヘッダー以外のデータの分割
- 容量管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4097ae3ab00bdf04ed2addff44b895bf9de31a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538897"
---
# <a name="header-data-split"></a>ヘッダー データの分割





このセクションでは、ヘッダー データの分割 NDIS 6.1 以降で利用できるサービスについて説明します。 *ヘッダー データが分割*を別のバッファーにヘッダーと受信のイーサネット フレーム内のデータを分割することでネットワークのパフォーマンスが向上します。 ヘッダーとデータを分離するには、メモリの領域が小さい方にまとめて収集するヘッダーができるようにします。 その結果、ヘッダーの詳細については、1 つのメモリ ページに収まるし、ドライバー スタックのメモリ アクセスのオーバーヘッドが軽減ように追加のヘッダーはシステム キャッシュに表示されます。

このセクションの内容:

[ヘッダー データの分割の概要](header-data-split-overview.md)

[ヘッダー データの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)

[イーサネット フレームの分割](splitting-ethernet-frames.md)

[受信ヘッダー データの分割を表示](receive-indications-with-header-data-split.md)

[ヘッダー データの分割の管理と構成](header-data-split-administration-and-configuration.md)

[プロトコル ドライバーおよびフィルター ドライバーでヘッダー データの分割のサポート](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)

 

 





