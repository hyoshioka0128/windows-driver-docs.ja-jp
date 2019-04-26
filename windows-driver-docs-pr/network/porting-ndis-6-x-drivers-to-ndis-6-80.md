---
title: NDIS 6.x ドライバーの NDIS 6.80 への移植
description: NDIS プロトコル、フィルター、および中間ドライバー、NDIS 6.80 は大幅に NDIS 6.60 と同じです。 NDIS 6.80 の新機能に関する詳細については、NDIS 6.80 の概要を参照してください。
ms.assetid: E5801DCE-B4D8-4BC6-B240-16BD9DB2B1F8
ms.date: 07/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8249bf6c9c4d7840d0560464d5a62017ef291cbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358717"
---
# <a name="porting-ndis-6x-drivers-to-ndis-680"></a>NDIS 6.x ドライバーの NDIS 6.80 への移植

NDIS ミニポート、プロトコル、フィルター、および中間ドライバー、NDIS 6.80 は大幅に NDIS 6.70 と同じです。 NIC ドライバーでは、NetAdapter クラス拡張 (NetAdapterCx) バージョン 1.1 で NDIS 6.80 に NDIS 6.70 でバージョン 1.0 からに更新されましたが。 NetAdapterCx する NDIS 6.x ミニポート ドライバーを移植するには、次を参照してください。 [NetAdapterCx に移植する NDIS ミニポート ドライバー](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md)します。

NDIS 6.80 の新機能に関する詳細についてなどの実装とコンパイルに固有の詳細、NDIS のこのバージョンを参照してください[NDIS 6.80 概要](introduction-to-ndis-6-80.md)します。

NDIS 6.x ミニポート、プロトコル、フィルター、または NDIS 6.80 に中間のドライバーを移植する場合は、変更 6.80 とドライバーのバージョンとの間には、各バージョンに慣れておく必要があります。 以前のバージョンの NDIS 6.x の詳細については、次のトピックを参照してください。

- [NDIS 6.70 の概要](introduction-to-ndis-6-70.md)
- [NDIS 6.60 の概要](introduction-to-ndis-6-60.md)
- [NDIS 6.50 の概要](introduction-to-ndis-6-50.md)
- [NDIS 6.40 の概要](introduction-to-ndis-6-40.md)
- [NDIS 6.30 の概要](introduction-to-ndis-6-30.md)
- [NDIS 6.20 が動作の概要](introduction-to-ndis-6-20.md)
- [NDIS 6.1 の概要](introduction-to-ndis-6-1.md)
- [NDIS 6.0 の概要](introduction-to-ndis-6-0.md)

