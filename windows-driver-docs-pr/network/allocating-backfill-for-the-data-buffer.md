---
title: データ バッファーのバックフィルの割り当て
description: データ バッファーのバックフィルの割り当て
ms.assetid: 2588986d-8d51-4f34-a3b9-d0df406afcba
keywords:
- ヘッダー データの分割 WDK、バックフィル割り当て
- バックフィル領域の割り当て WDK ヘッダー以外のデータを分割します。
- 事前に割り当てられたバックフィル storage WDK のヘッダー データの分割
- バックフィルのデータ領域 WDK ヘッダー以外のデータの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 226ce041f1509f86f82514932429447adcdcbede
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386360"
---
# <a name="allocating-backfill-for-the-data-buffer"></a>データ バッファーのバックフィルの割り当て





NDIS ミニポート ドライバーに割り当てる必要がありますデータ バックフィルの領域の量を指定する、 **BackfillSize**のメンバー、 [ **NDIS\_HD\_分割\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_hd_split_attributes)構造体。 ヘッダー データの分割の属性を設定する方法についての詳細については、次を参照してください。[ヘッダー データの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)します。

ミニポート ドライバーが、少なくとものバックフィル記憶域を割り当てる必要があります事前 NIC では、ヘッダーと受信したイーサネット フレーム内のデータを分割、ときにバイト数を**BackfillSize**前のデータ部分の開始アドレスに、を指定します、フレーム。 バックフィル ストレージがページ境界を越えないする必要があります。

ドライバー スタックは、フレームのヘッダー部分をコピーし、イーサネット フレームの分割処理できないネットワークのドライバーの事実上の連続フレームを作成する、事前に割り当てられたバックフィル記憶域を使用できます。

 

 





