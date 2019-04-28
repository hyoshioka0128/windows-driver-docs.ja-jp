---
title: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
description: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
ms.assetid: 57E22B53-5ECC-4B4C-8A98-C1125314868B
keywords:
- NDIS_STATUS_WWAN_BASE_STATIONS_INFO、ベース ステーション情報クエリの状態の通知、モバイル ブロード バンド基地局情報クエリの状態の通知、MB 基地局情報のクエリ状態通知
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdfb122201656f58a84db7b54042ef94c7e5479d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369897"
---
# <a name="ndisstatuswwanbasestationsinfo"></a>NDIS_STATUS_WWAN_BASE_STATIONS_INFO

モデムのミニポート ドライバーへの応答で NDIS_STATUS_WWAN_BASE_STATIONS_INFO 通知が送信される、 [OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md) MB ホストを提供していると、近隣の両方に関する情報を提供するクエリ要求ステーションをベースします。

この通知を使用して、 [NDIS_WWAN_BASE_STATIONS_INFO](https://msdn.microsoft.com/library/windows/hardware/7C0E0903-F564-4F2B-95F9-FA8512FEF61B)構造体。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>関連項目

[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://msdn.microsoft.com/library/windows/hardware/7C0E0903-F564-4F2B-95F9-FA8512FEF61B)

[MB ベース ステーション情報のクエリ操作](mb-base-stations-information-query-support.md)

