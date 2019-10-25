---
title: フィルター モジュールの送信および受信操作
description: フィルター モジュールの送信および受信操作
ms.assetid: 208f9af6-cde4-4801-9355-daa6633d7d0b
keywords:
- フィルターモジュール WDK ネットワーク、送信操作
- フィルターモジュール WDK ネットワーク, 受信操作
- フィルタードライバーの WDK ネットワーク、送信操作
- NDIS フィルタードライバー WDK、send 操作
- フィルタードライバー WDK ネットワーク, 受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e930c8a7eae4d3f38f9c4596c045b65acac7ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838105"
---
# <a name="filter-module-send-and-receive-operations"></a>フィルター モジュールの送信および受信操作





このセクションでは、NDIS 6.0 フィルタードライバーの送信および受信操作について説明します。 フィルタードライバーは、送信要求を開始し、通知を受信したり、他のドライバーの要求や表示をフィルター処理したりすることができます。

フィルターモジュールは、ミニポートアダプター上に積み重ねられます。 ドライバースタックの詳細については、「 [NDIS 6.0 ドライバースタック](ndis-driver-stack.md)」を参照してください。

ドライバースタック内のフィルターモジュールは、すべての送信要求をフィルター処理し、基になるアダプターに関連付けられている表示を受け取ることができます。 これは、アダプターへのすべてのプロトコルバインドに当てはまります。 NDIS 6.0 送受信操作の詳細については、「[送信および受信操作](send-and-receive-operations.md)」を参照してください。

フィルタードライバーは、 [**NDIS\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造に基づく従来の送信および受信操作を直接サポートしていません。 代わりに、NDIS は従来のミニポートドライバーからの受信通知を[**NET\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造に変換します。 また、NDIS は、NET\_バッファー構造に基づく送信要求から、NDIS\_パケット構造に基づくレガシ送信要求への必要な変換を処理します。

フィルタードライバーでは、フィルターモジュールの*送信関数と*受信フィルターモジュールを動的に変更できる  に**注意**してください。 詳細については、「[データバイパスモード](data-bypass-mode.md)」を参照してください。

 

次のトピックでは、フィルタードライバーの送信操作と受信操作に関する追加情報を提供します。

[フィルタードライバーのバッファー管理](filter-driver-buffer-management.md)

[フィルタードライバーからのデータの送信](sending-data-from-a-filter-driver.md)

[フィルタードライバーでの送信要求のキャンセル](canceling-a-send-request-in-a-filter-driver.md)

[フィルタードライバーでのデータの受信](receiving-data-in-a-filter-driver.md)

 

 





