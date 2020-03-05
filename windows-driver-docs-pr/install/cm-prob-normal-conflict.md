---
title: CM_PROB_NORMAL_CONFLICT
description: CM_PROB_NORMAL_CONFLICT
ms.assetid: 18c5ca02-0a4c-4a0e-8b33-5c685a73d4c8
keywords:
- CM_PROB_NORMAL_CONFLICT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8dabe519441bf0a0f77196ea39b249e51284268
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279512"
---
# <a name="code-12---cm_prob_normal_conflict"></a>コード 12-CM_PROB_NORMAL_CONFLICT

このデバイスマネージャーエラーメッセージは、2つのデバイスに同じ i/o ポート、同じ割り込み、または同じ DMA チャネル (BIOS、オペレーティングシステム、またはそれらの組み合わせによって) が割り当てられていることを示します。

## <a name="error-code"></a>エラー コード

12

### <a name="display-message"></a>メッセージの表示

"このデバイスは、使用できる十分な空きリソースを見つけることができません。 (コード 12)

"このデバイスを使用する場合は、このシステム上の他のデバイスの1つを無効にする必要があります。"

### <a name="recommended-resolution"></a>推奨される解決策

[デバイスマネージャーを使用](using-device-manager.md)して、競合の原因を特定し、競合を解決します。 デバイスの競合を解決する方法の詳細については、デバイスマネージャーの使用方法に関するヘルプ情報を参照してください。

このエラーメッセージは、BIOS によってデバイスに十分なリソースが割り当てられなかった場合にも表示されます。 たとえば、BIOS が無効なマルチプロセッサ仕様 (MP) テーブルによって USB コントローラーに割り込みを割り当てない場合に、このメッセージが表示されます。
