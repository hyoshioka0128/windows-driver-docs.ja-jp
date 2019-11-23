---
title: NDIS 6.1 データ構造の使用
description: NDIS 6.1 データ構造の使用
ms.assetid: 425cd2dc-99b0-4bed-8f7b-c291769c420a
keywords:
- データ構造の WDK ネットワーク
- NDIS WDK、構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2392aee51206faf58a5bec34dc9173a7e56563b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842987"
---
# <a name="using-ndis-61-data-structures"></a>NDIS 6.1 データ構造の使用





NDIS では、同じデータ構造の複数のバージョンをサポートできます。 Windows Server 2008、Windows Vista Service Pack 1 (SP1)、または両方のオペレーティングシステムで更新された構造を使用する NDIS 6.1 ドライバーでは、ndis 6.1 データ構造体の初期化時に、構造体の**ヘッダー**メンバー (存在する場合) のヘッダー構造に含まれる、正しい**リビジョン**メンバーと**サイズ**のメンバー [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)値を報告する必要があります。

**注**  正しいバージョンとサイズの情報を確認するには、**ヘッダー**メンバーを含む各構造の参照ページを参照してください。 **ヘッダー**メンバーを含み、ndis 6.1 用に更新された構造体の参照ページには、ndis 6.1 ドライバーの新しい情報が含まれています。 Ndis 6.1 の構造が更新されていない場合は、ndis 6.0 ドライバー用に提供されている情報が NDIS 6.1 ドライバーにも適用されます。

 

 

 





