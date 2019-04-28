---
title: NDIS 6.1 の Direct OID 要求インターフェイス
description: NDIS 6.1 の Direct OID 要求インターフェイス
ms.assetid: 1a24dec6-f16a-45f5-857b-c6e0df4ce261
keywords:
- 直接の OID 要求インターフェイス WDK ネットワーク
- 直接の OID 要求パスの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925ce2225b19e0b3c22d72ebf992bf19da9a4804
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379575"
---
# <a name="direct-oid-request-interface-in-ndis-61"></a>NDIS 6.1 の Direct OID 要求インターフェイス





NDIS は、NDIS 6.1 と以降のドライバーの直接の OID 要求インターフェイスを提供します。 *OID の直接の要求パス*クエリを実行したり、頻繁に設定されている OID 要求をサポートします。 IPsec のバージョン 2 (IPsecOV2) オフロードなどのインターフェイスを提供、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812)直接 OID 要求の OID。

直接の OID 要求インターフェイスは、NDIS ドライバーでは省略可能。 OID の直接パスをサポートするドライバーがエントリ ポイントを提供し、NDIS 提供**Ndis * Xxx*** プロトコル、フィルター、およびミニポートのドライバーの関数。

**注**  NDIS は、OID 要求インターフェイスを直接使用するための特定の Oid をサポートしています。 ドライバーが Oid の直接のインターフェイスの OID を使用できるかどうかを確認するには、OID のリファレンス ページで、ノートを参照してください。

 

NDIS 6.1、IPsecOV2 は直接の OID 要求インターフェイスを使用する唯一のインターフェイスです。 IPsecOV2 の詳細については、次を参照してください。 [IPsec タスク オフロード バージョン 2 で NDIS 6.1](ipsec-task-offload-version-2-in-ndis-6-1.md)します。

Windows Server 2008 および Windows Vista Service Pack 1 (SP1) オペレーティング システムとドライバーを NDIS 6.1、OID 要求インターフェイスを直接、次のアルゴリズムのみを使用できます。

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_UPDATE\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569814)

ミニポート ドライバーとフィルター ドライバーはシリアル化されないを直接の OID 要求を処理できる必要があります。 標準の OID 要求インターフェイスとは異なり NDIS は他の OID の直接のインターフェイスと標準の OID 要求インターフェイスに送信される要求との直接の OID 要求をシリアル化できません。 また、ミニポート ドライバーとフィルター ドライバーできる必要があります IRQL で直接 OID 要求を処理するために&lt;= ディスパッチ\_レベル。

ドライバーの OID の直接のインターフェイスを実装する方法の詳細については、次のトピックを参照してください。

-   [ミニポート アダプタの OID 要求](miniport-adapter-oid-requests.md)

-   [プロトコル ドライバー OID 要求](protocol-driver-oid-requests.md)

-   [モジュールの OID 要求をフィルター処理します。](filter-module-oid-requests.md)

 

 





