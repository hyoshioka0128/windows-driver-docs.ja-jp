---
title: バックフィルをデータ バッファーの割り当てください。
description: バックフィルをデータ バッファーの割り当てください。
ms.assetid: 2588986d-8d51-4f34-a3b9-d0df406afcba
keywords:
- ヘッダー データの分割 WDK、バックフィル割り当て
- バックフィル領域の割り当て WDK ヘッダー以外のデータを分割します。
- 事前に割り当てられたバックフィル storage WDK のヘッダー データの分割
- バックフィルのデータ領域 WDK ヘッダー以外のデータの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed03f808baab51a3dd6bb47581b6717a9b6b90f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559019"
---
# <a name="allocating-backfill-for-the-data-buffer"></a>バックフィルをデータ バッファーの割り当てください。





NDIS ミニポート ドライバーに割り当てる必要がありますデータ バックフィルの領域の量を指定する、 **BackfillSize**のメンバー、 [ **NDIS\_HD\_分割\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)構造体。 ヘッダー データの分割の属性を設定する方法についての詳細については、次を参照してください。[ヘッダー データの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)します。

ミニポート ドライバーが、少なくとものバックフィル記憶域を割り当てる必要があります事前 NIC では、ヘッダーと受信したイーサネット フレーム内のデータを分割、ときにバイト数を**BackfillSize**前のデータ部分の開始アドレスに、を指定します、フレーム。 バックフィル ストレージがページ境界を越えないする必要があります。

ドライバー スタックは、フレームのヘッダー部分をコピーし、イーサネット フレームの分割処理できないネットワークのドライバーの事実上の連続フレームを作成する、事前に割り当てられたバックフィル記憶域を使用できます。

 

 





