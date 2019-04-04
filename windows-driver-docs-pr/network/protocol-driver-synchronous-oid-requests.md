---
title: プロトコル ドライバーの同期の OID を要求
description: このトピックでは、ミニポート アダプター同期 OID 要求を説明します。
ms.assetid: 34B88444-DDF1-4AEA-8277-3EA87CA7004A
keywords: プロトコル ドライバー OID 要求インターフェイス、同期プロトコル driverSynchronous OID 呼び出しプロトコル driverWDK 同期 Oid、プロトコル driverSynchronous OID 要求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2744d5b295dcaf08f9e5c76bf01bd212ce101d98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538004"
---
# <a name="protocol-driver-synchronous-oid-requests"></a>プロトコル ドライバーの同期の OID を要求

同期の OID の要求パスをサポートするプロトコルのドライバーの呼び出し、 [ **NdisSynchronousOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/BF539DDA-59ED-4010-88BC-3C7D8DC475EF)同期 OID を発行する関数。

プロトコルのドライバー、*同期 OID 要求インターフェイス*とは異なり、標準モードと直接 OID 要求インターフェイス プロトコル ドライバーを非同期に実装する必要はありません*完了*コールバック関数。 これは、パスの同期の性質のためです。 [全般] では、通常、直接、および同期の Oid との違いについての詳細については、[同期 OID 要求インターフェイスで NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)を参照してください。

> [!NOTE]
> NDIS 6.80 には、同期の OID 要求インターフェイスで使用するための特定の Oid がサポートされています。 NDIS 6.80 といくつかの NDIS 6.80 Oid がサポートされていません前に存在する Oid。 同期の OID 要求インターフェイスの OID を使用できるかどうかを確認するには、OID のリファレンス ページを参照してください。

同期 OID 要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表では、同期の OID 要求インターフェイスでの機能と標準の OID 要求インターフェイス間のリレーションシップを示します。

| 同期の OID 関数 | 標準の OID 関数 |
| --- | --- |
| [*NdisSynchronousOidRequest*](https://msdn.microsoft.com/library/windows/hardware/BF539DDA-59ED-4010-88BC-3C7D8DC475EF) | [*NdisOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff563710) |

