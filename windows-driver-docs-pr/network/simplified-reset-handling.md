---
title: 簡略化されたリセット処理
description: 簡略化されたリセット処理
ms.assetid: ac07bfe3-9144-422a-96ca-d2ca2cc6861d
keywords:
- NDIS ミニポート ドライバー WDK、ミニポート アダプターをリセットします。
- ミニポート アダプターをリセットします。
- アダプターの WDK ネットワー キング、リセットの操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d01b62f1e761d1eb962061bf45ad15a206f48675
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356857"
---
# <a name="simplified-reset-handling"></a>簡略化されたリセット処理





NDIS 6.0 とそれ以降のドライバー、キャンセルの送信または OID 要求ミニポート アダプターはリセットされません。 代わりに、NDIS な OID 要求の送信のキャンセル機能とキャンセル機能できます。

NDIS ミニポート ドライバーは、完了または保留中の送信操作をキャンセルまたは OID 保留中の要求 - いつでも前に、または後のリセットを完了できます。 ミニポート ドライバーには、リセットに対して要求を受信したときを追跡するのにはありません。 また、ドライバーはリセットを完了に取り消された要求を同期する必要はありません。

詳細については、次を参照してください[送信操作のキャンセル](canceling-a-send-operation.md)、[アダプターの OID 要求](miniport-adapter-oid-requests.md)、[プロトコル ドライバー OID 要求](protocol-driver-oid-requests.md)、および[フィルター モジュールの OID。要求](filter-module-oid-requests.md)します。

 

 





