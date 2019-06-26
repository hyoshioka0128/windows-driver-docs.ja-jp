---
title: ミニポートアダプター同期 OID 要求
description: このトピックでは、ミニポート アダプター同期 OID 要求を説明します。
ms.assetid: E169972C-2EFF-4005-B279-9EFC53B431E2
keywords: ミニポート アダプター同期 OID 要求インターフェイス、ミニポート アダプター同期 OID 呼び出し、WDK ミニポート アダプター同期 Oid、ミニポート アダプター同期 OID 要求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ada6ec85a15c9724921e0ad82133723dca707cb4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373936"
---
# <a name="miniport-adapter-synchronous-oid-requests"></a>ミニポートアダプター同期 OID 要求

ミニポート ドライバーを提供する同期の OID の要求パスをサポートするために、 [ *MiniportSynchronousOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-miniport_synchronous_oid_request)関数内のエントリ ポイント、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の呼び出し時に構造体、 [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)関数。

ミニポート ドライバーについて、*同期 OID 要求インターフェイス*とは異なり、標準モードと直接 OID 要求インターフェイスのミニポート ドライバーを非同期に登録する必要はありません*完了*コールバック関数。 これは、パスの同期の性質のためです。 [全般] では、通常、直接、および同期の Oid との違いについての詳細については、次を参照してください。[同期 OID 要求インターフェイスで NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)します。

> [!NOTE]
> NDIS 6.80 には、同期の OID 要求インターフェイスで使用するための特定の Oid がサポートされています。 NDIS 6.80 といくつかの NDIS 6.80 Oid がサポートされていません前に存在する Oid。 同期の OID 要求インターフェイスの OID を使用できるかどうかを確認するには、OID のリファレンス ページを参照してください。

同期 OID 要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表では、同期の OID 要求インターフェイスでの機能と標準の OID 要求インターフェイス間のリレーションシップを示します。

| 同期の OID 関数 | 標準の OID 関数 |
| --- | --- |
| [*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-miniport_synchronous_oid_request) | [*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request) |

