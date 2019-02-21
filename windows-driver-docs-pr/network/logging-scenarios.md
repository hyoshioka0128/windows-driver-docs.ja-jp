---
title: ログ記録シナリオ
description: このトピックでは、WDI ドライバーでのログ記録 IHV トレースでユーザーが開始したフィードバックのログ記録シナリオについて説明します。
ms.assetid: B9E10527-9C25-46B6-ADC2-4CF5AB749E04
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5397717ab4f81be578f50c105f560db489d4a000
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530380"
---
# <a name="logging-scenarios"></a>ログ記録シナリオ

再現コード モードおよび自動ロガーの両方に対して、IHV ログ ファイルに保存するイベントは、ことを確認するには少なくとも 30 分間のログ イベントが常に保存する過去のフラグ、レベルとキーワードを使用して、適切に調整する必要があります。 実際には、対象に 1 つのスキャン/WFD 検出、1 つの接続/移動イベントに対応する期間の 30 分間にする必要があります、いずれかのイベント、いくつか power 遷移、および 10 分の送信接続を切断し、データを受信します。 IHV 再現コード モードは、ログははるかに通常の IHV 自動-ロガーを超えるためより詳細なログ記録が必要です。

ログインするときに、次のシナリオでは役立つ場合があります。

- 接続を取得します。
- 電源の遷移
- ラジオの管理
- Roaming
- ハング/復旧
- 制限に接続してから移行します。

## <a name="related-links"></a>関連リンク

[IHV のトレース ログ記録でフィードバックをユーザーが開始しました。](user-initiated-feedback-with-ihv-trace-logging.md)
