---
title: プロトコル ドライバー同期 OID 要求
description: このトピックでは、ミニポートアダプターの同期 OID 要求について説明します。
ms.assetid: 34B88444-DDF1-4AEA-8277-3EA87CA7004A
keywords: プロトコルドライバー同期 OID 要求インターフェイス、プロトコル driverSynchronous OID 呼び出し、プロトコル Driversynchronous 同期 oid、プロトコル driverSynchronous OID 要求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8dc84c841a9c5fed135ad43c34d7e54374a54a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844905"
---
# <a name="protocol-driver-synchronous-oid-requests"></a>プロトコル ドライバー同期 OID 要求

同期 OID 要求パスをサポートするために、プロトコルドライバーは[**NdisSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest)関数を呼び出して同期 oid を発行します。

プロトコルドライバーの場合、*同期 oid 要求インターフェイス*は、非同期の*完全な*コールバック関数を実装する必要がないという点で、通常および直接の oid 要求インターフェイスと異なります。 これは、パスの同期的な性質によるものです。 標準、直接、および同期 Oid の一般的な相違点の詳細については、「 [NDIS 6.80 の同期 Oid 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)」を参照してください。

> [!NOTE]
> NDIS 6.80 では、同期 OID 要求インターフェイスで使用する特定の Oid がサポートされています。 NDIS 6.80 および一部の NDIS 6.80 Oid より前に存在していた Oid はサポートされていません。 同期 OID 要求インターフェイスで OID を使用できるかどうかを判断するには、「OID リファレンス」ページを参照してください。

同期 OID 要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表は、同期 OID 要求インターフェイスの関数と標準 OID 要求インターフェイスの間の関係を示しています。

| 同期 OID 関数 | 標準 OID 関数 |
| --- | --- |
| [*NdisSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest) | [*NdisOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) |

