---
title: ミニポートアダプター同期 OID 要求
description: このトピックでは、ミニポートアダプターの同期 OID 要求について説明します。
ms.assetid: E169972C-2EFF-4005-B279-9EFC53B431E2
keywords: ミニポートアダプター同期 OID 要求インターフェイス、ミニポートアダプター同期 OID 呼び出し、WDK ミニポートアダプター同期 oid、ミニポートアダプター同期 OID 要求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6b055941a4ed1da1bd033b4d3d3ee85bf796387
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844241"
---
# <a name="miniport-adapter-synchronous-oid-requests"></a>ミニポートアダプター同期 OID 要求

同期 OID 要求パスをサポートするために、ミニポートドライバーは、 [*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request)関数のエントリ[ **\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)ポイントを提供し[**ます。NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数。

ミニポートドライバーの場合、*同期 oid 要求インターフェイス*は、ミニポートドライバーで非同期*完了*コールバック関数を登録する必要がないので、通常および直接の oid 要求インターフェイスと異なります。 これは、パスの同期的な性質によるものです。 標準、直接、および同期 Oid の一般的な相違点の詳細については、「 [NDIS 6.80 の同期 Oid 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)」を参照してください。

> [!NOTE]
> NDIS 6.80 では、同期 OID 要求インターフェイスで使用する特定の Oid がサポートされています。 NDIS 6.80 および一部の NDIS 6.80 Oid より前に存在していた Oid はサポートされていません。 同期 OID 要求インターフェイスで OID を使用できるかどうかを判断するには、「OID リファレンス」ページを参照してください。

同期 OID 要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表は、同期 OID 要求インターフェイスの関数と標準 OID 要求インターフェイスの間の関係を示しています。

| 同期 OID 関数 | 標準 OID 関数 |
| --- | --- |
| [*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request) | [*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) |

