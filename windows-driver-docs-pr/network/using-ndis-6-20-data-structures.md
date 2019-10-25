---
title: NDIS 6.20 データ構造の使用
description: NDIS 6.20 データ構造の使用
ms.assetid: 19810a7c-91c1-4014-a364-2819d743627d
keywords:
- NDIS 6.20 WDK、データ構造体
- データ構造 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdaad950481937d5a9a68af017c9c1b96130b6c8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842985"
---
# <a name="using-ndis-620-data-structures"></a>NDIS 6.20 データ構造の使用





NDIS では、同じデータ構造の複数のバージョンをサポートできます。 更新された構造体を使用する NDIS 6.20 以降のドライバーは、構造体の**ヘッダー**メンバー (存在する場合) に含まれる[**ヘッダー構造\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)構造体の正しい**リビジョン**メンバーと**サイズ**のメンバー\_値を報告する必要があります。ドライバーが NDIS 6.20 データ構造体を初期化するとき。

**注**  正しいバージョンとサイズの情報を確認するには、**ヘッダー**メンバーを含む各構造の参照ページを参照してください。 **ヘッダー**メンバーを含み、ndis 6.20 用に更新された構造体の参照ページには、ndis 6.20 以降のドライバーに関する新しい情報が含まれています。 Ndis 6.20 の構造が更新されていない場合、ndis 6.0 または NDIS 6.1 ドライバーに提供されている情報は、NDIS 6.20 以降のドライバーにも適用されます。

 

 

 





