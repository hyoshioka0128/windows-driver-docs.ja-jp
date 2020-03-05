---
title: CM_PROB_WAITING_ON_DEPENDENCY
description: CM_PROB_WAITING_ON_DEPENDENCY
ms.assetid: 2f45c507-1926-47f4-aca8-f8b834c58601
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d7cc2065e74f7c1521e40e098f7e53a69879537
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279465"
---
# <a name="code-51---cm_prob_waiting_on_dependency"></a>コード 51-CM_PROB_WAITING_ON_DEPENDENCY

このデバイスマネージャーエラーメッセージは、デバイスが開始されていない別のデバイスに依存しているため、デバイスが起動しなかったことを示します。

## <a name="error-code"></a>エラー コード

51

### <a name="display-message"></a>メッセージの表示

"このデバイスは、現在、別のデバイスまたはデバイスのセットの開始を待機しています。 (コード 51)。 "

### <a name="recommended-resolution"></a>推奨される解決策

現在、この問題に対する解決策はありません。

問題の診断に役立てるために、このデバイスが依存している可能性のあるデバイス[ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)内の他の障害が発生しているデバイスを確認します。 別の関連デバイスが開始されなかった理由を特定できる場合は、この問題を解決できる可能性があります。
