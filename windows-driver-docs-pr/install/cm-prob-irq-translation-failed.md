---
title: CM_PROB_IRQ_TRANSLATION_FAILED
description: CM_PROB_IRQ_TRANSLATION_FAILED
ms.assetid: fafd40d5-43bf-4243-907a-df523e1b501e
keywords:
- CM_PROB_IRQ_TRANSLATION_FAILED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d8dc6769ed69c7b6a1b9e9d4d840ea02b0ea211
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279536"
---
# <a name="code-36---cm_prob_irq_translation_failed"></a>コード 36-CM_PROB_IRQ_TRANSLATION_FAILED

このデバイスマネージャーエラーメッセージは、デバイスの IRQ 変換に失敗したことを示します。

## <a name="error-code"></a>エラー コード

36

### <a name="display-message"></a>メッセージの表示

"このデバイスは PCI 割り込みを要求していますが、ISA の割り込み用に構成されています (またはその逆)。 このデバイスの割り込みを再構成するには、コンピューターのシステムセットアッププログラムを使用してください。 (コード 36) "

### <a name="recommended-resolution"></a>推奨される解決策

BIOS セットアップユーティリティを使用して、IRQ 予約の設定を変更してみます (このオプションが存在する場合)。 (BIOS に PCI または ISA デバイスの特定の Irq を予約するオプションがある場合があります)。
