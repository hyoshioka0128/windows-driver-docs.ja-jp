---
title: CM_PROB_FAILED_POST_START
description: CM_PROB_FAILED_POST_START
ms.assetid: 82d43c8b-d5de-4395-9ca0-34d2258b9772
keywords:
- CM_PROB_FAILED_POST_START
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54b4df29184de0203e117d31d1777dd9a0b51882
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580533"
---
# <a name="cmprobfailedpoststart"></a>CM_PROB_FAILED_POST_START

この関数は、システムの使用に予約されています。

ドライバーが、デバイス エラーを報告します。

## <a name="error-code"></a>エラー コード

43

### <a name="display-message"></a>メッセージを表示します。

"Windows が停止しましたこのデバイスの問題が発生したので。 (コード 43)"

### <a name="recommended-resolution"></a>推奨される解決方法

アンインストールし、デバイスを再インストールします。

デバイスを制御するドライバーの 1 つは指示 IRP_MN_QUERY_PNP_DEVICE_STATE への応答でなんらかの方法で、デバイスが失敗しました、オペレーティング システムです。
