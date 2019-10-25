---
title: データ バッファーのバックフィルの割り当て
description: データ バッファーのバックフィルの割り当て
ms.assetid: 2588986d-8d51-4f34-a3b9-d0df406afcba
keywords:
- ヘッダー-データ分割 WDK、バックフィルの割り当て
- バックフィル領域の割り当て WDK ヘッダー-データの分割
- 事前に割り当てられたバックフィルストレージ WDK ヘッダー-データ分割
- データのバックフィル領域 WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 524ff4899573d2b2c9d73136b2961fa384546eeb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835315"
---
# <a name="allocating-backfill-for-the-data-buffer"></a>データ バッファーのバックフィルの割り当て





NDIS は、ミニポートドライバーが[**ndis\_HD\_SPLIT\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)構造体の**backfillsize**メンバーで割り当てる必要があるデータのバックフィル領域の量を指定します。 ヘッダーデータの分割属性の設定の詳細については、「[ヘッダーデータの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)」を参照してください。

NIC が、受信したイーサネットフレーム内のヘッダーとデータを分割する場合、ミニポートドライバーは、少なくとも**Backfillsize**がフレームのデータ部分の開始アドレスの前に指定するバイト数以上のバックフィルストレージを事前に割り当てている必要があります。 バックフィルストレージは、ページの境界を越えることはできません。

ドライバースタックは、事前に割り当てられたバックフィルストレージを使用してフレームのヘッダー部分をコピーし、分割イーサネットフレームを処理できないネットワークドライバー用に事実上連続したフレームを作成できます。

 

 





