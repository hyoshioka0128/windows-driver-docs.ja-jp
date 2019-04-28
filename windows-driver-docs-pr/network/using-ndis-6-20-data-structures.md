---
title: NDIS 6.20 データ構造の使用
description: NDIS 6.20 データ構造の使用
ms.assetid: 19810a7c-91c1-4014-a364-2819d743627d
keywords:
- NDIS 6.20 WDK、データ構造体
- WDK NDIS 6.20 が動作のデータ構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83a02ed132802747945b64f334588f7767e9f80f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372102"
---
# <a name="using-ndis-620-data-structures"></a>NDIS 6.20 データ構造の使用





NDIS は、同じデータ構造体の複数のバージョンをサポートできます。 NDIS 6.20 が動作し、更新された構造体を使用する以降のドライバーは、適切な報告する必要があります**リビジョン**メンバーと**サイズ**でメンバーの値、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)構造内にある、**ヘッダー**ドライバー NDIS 6.20 データ構造を初期化するときに存在する場合の構造体のメンバー。

**注**  適切なバージョンおよびサイズの情報を含む各構造のリファレンス ページを参照してください。 を決定する、**ヘッダー**メンバー。 含む構造体のリファレンス ページを**ヘッダー**メンバーとするが更新された NDIS 6.20 が NDIS 6.20 が動作し、以降のドライバーの新しい情報が含まれます。 NDIS 6.20 が動作の構造体への更新プログラムがない場合は、NDIS 6.0 または NDIS 6.1 ドライバー提供される情報は、NDIS 6.20 が動作し、以降のドライバーにも当てはまります。

 

 

 





