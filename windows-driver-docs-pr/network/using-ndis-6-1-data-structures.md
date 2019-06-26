---
title: NDIS 6.1 データ構造の使用
description: NDIS 6.1 データ構造の使用
ms.assetid: 425cd2dc-99b0-4bed-8f7b-c291769c420a
keywords:
- データ構造体の WDK ネットワーク
- NDIS WDK、構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81058681da218df199f292adad775bf25d6e7dc5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360727"
---
# <a name="using-ndis-61-data-structures"></a>NDIS 6.1 データ構造の使用





NDIS は、同じデータ構造体の複数のバージョンをサポートできます。 使用する NDIS 6.1 ドライバーが Windows Server 2008、Windows Vista Service Pack 1 (SP1) で構造を更新または両方のオペレーティング システムは、適切な報告する必要があります**リビジョン**メンバーと**サイズ**でメンバー値[ **NDIS\_オブジェクト\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)構造内にある、**ヘッダー**存在する場合の構造体のメンバーとドライバーNDIS 6.1 データ構造を初期化します。

**注**  適切なバージョンおよびサイズの情報を確認するのを含む各構造のリファレンス ページを参照してください、**ヘッダー**メンバー。 含む構造体のリファレンス ページを**ヘッダー**メンバーとするが更新された NDIS 6.1 に NDIS 6.1 ドライバーの新しい情報が含まれます。 NDIS 6.1 の構造体への更新プログラムがない場合は、NDIS 6.0 のドライバーに対して提供される情報は、NDIS 6.1 ドライバーにも当てはまります。

 

 

 





