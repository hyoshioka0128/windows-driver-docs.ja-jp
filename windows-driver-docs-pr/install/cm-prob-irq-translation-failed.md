---
title: CM_PROB_IRQ_TRANSLATION_FAILED
description: CM_PROB_IRQ_TRANSLATION_FAILED
ms.assetid: fafd40d5-43bf-4243-907a-df523e1b501e
keywords:
- CM_PROB_IRQ_TRANSLATION_FAILED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0900e559e0fd8ad4172befb8fabb0fecf54c668
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355767"
---
# <a name="cmprobirqtranslationfailed"></a>CM_PROB_IRQ_TRANSLATION_FAILED

この関数は、システムの使用に予約されています。

デバイスの IRQ 変換に失敗しました。

## <a name="error-code"></a>エラー コード

36

### <a name="display-message"></a>メッセージを表示します。

"このデバイスは、PCI 割り込みを要求しているが、ISA、割り込みの (またはその逆) が構成されています。 このデバイスに対する割り込みを再構成するのにコンピューターのシステムのセットアップ プログラムを使用してください。 (コード 36)"

### <a name="recommended-resolution"></a>推奨される解決方法

このようなオプションが存在する場合は、IRQ の予約の設定を変更する、BIOS セットアップ ユーティリティを使用してください。 (BIOS は、PCI、ISA のデバイスの特定の Irq を予約するためのオプションがあります)
