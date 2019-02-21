---
title: PTP エラーからの回復
description: PTP エラーからの回復
ms.assetid: 0f89d6b6-9d95-4e98-aa90-08c9508a2228
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f17076f041998e16e8100aaff94c6bd97cf8957
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553666"
---
# <a name="ptp-error-recovery"></a>PTP エラーからの回復





Microsoft PTP クラスのミニドライバーの初期化中に (つまりの初期の取得 DeviceInfo と ObjectInfo データセット、およびプロパティの説明)、エラーは致命的なエラーとして扱われ、WIA ミニドライバーが初期化に失敗します。

(たとえば、イメージの取得) 中、後で処理中に Microsoft PTP ミニドライバーが最初 (USB まだイメージ キャプチャ デバイスの定義で説明) デバイスの状態の USB の取得クラスに固有の要求を送信しようと認識できないエラーが発生したときに. その要求が成功すると、ドライバーは停止しているエンドポイントをクリアし、続行します。

デバイスの状態の取得要求が失敗した場合、PTP ミニドライバーは、デバイスをリセット クラス固有の要求が (USB まだイメージ キャプチャ デバイスの定義で説明) を使用してデバイスをリセットしようとします。 クラス固有のデバイスのリセット要求が成功したかどうかに返されます S\_S ではなく FALSE\_ok をクリックします。 デバイスをリセットに失敗した場合、クラス固有のデバイスのリセット要求はエラー コードを返します。

 

 




