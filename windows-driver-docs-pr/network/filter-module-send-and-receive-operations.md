---
title: フィルター モジュールの送信し、受信操作
description: フィルター モジュールの送信し、受信操作
ms.assetid: 208f9af6-cde4-4801-9355-daa6633d7d0b
keywords:
- モジュールの WDK ネットワークをフィルター処理、送信操作
- モジュールの WDK ネットワークをフィルター処理、受信操作
- ドライバー WDK ネットワークをフィルター処理、送信操作
- NDIS フィルター ドライバー WDK、送信操作
- ドライバー WDK ネットワークをフィルター処理、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dfb8e01286a1388539682859872f290d97ed16d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557517"
---
# <a name="filter-module-send-and-receive-operations"></a>フィルター モジュールの送信し、受信操作





このセクションのドキュメントは、NDIS 6.0 フィルター ドライバーの操作を送受信します。 フィルター ドライバーは、送信要求の開始し受信表示または要求およびその他のドライバーの兆候をフィルター処理できます。

フィルター モジュールは、ミニポート アダプタ上でスタックされます。 ドライバー スタックの詳細については、[NDIS 6.0 ドライバー スタック](ndis-driver-stack.md)を参照してください。

ドライバー スタック内のフィルター モジュールでは、すべての送信要求をフィルター処理でき、基になるアダプターに関連付けられているインジケーターを受信することができます。 これは、すべてのプロトコル バインドをアダプターに当てはまります。 NDIS 6.0 の詳細については送信し受信操作を参照してください[送信および受信操作](send-and-receive-operations.md)します。

フィルター ドライバーはいない direct サポートは、従来の送信および受信操作に基づく、 [ **NDIS\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff557086)構造体。 NDIS に変換が従来のミニポート ドライバーにからインジケーターを受信する代わりに、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。 NDIS が NET に基づく送信要求からの必要な変換を処理することも、\_レガシ バッファーの構造体は、NDIS に基づく要求を送信\_パケットの構造体。

**注**  フィルター ドライバーは、送信を変更したり、受信*FliterXxx*フィルター モジュールを動的に機能します。 詳細については、[データ バイパス モード](data-bypass-mode.md)を参照してください。

 

次のトピックでは、フィルター ドライバーの送信に関する追加情報を提供し、受信処理。

[フィルター ドライバー バッファー管理](filter-driver-buffer-management.md)

[フィルター ドライバーからデータを送信します。](sending-data-from-a-filter-driver.md)

[フィルター ドライバーでは、送信要求を取り消す](canceling-a-send-request-in-a-filter-driver.md)

[フィルター ドライバーのデータの受信](receiving-data-in-a-filter-driver.md)

 

 





