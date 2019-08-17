---
title: IHV トレースログを使用したユーザーによるフィードバックの概要
description: このセクションのこのトピックでは、フィードバックツールを使用して送信されたユーザーによるフィードバック (UIF) レポートで、詳細な IHV トレースログを収集するために必要な手順の概要を示します。
ms.assetid: BDD02AA2-A771-4AC1-B9D2-E9E8FA073B7A
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1910110cc2507a08ece4bbb8ed717b63341eaa98
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565694"
---
# <a name="user-initiated-feedback-with-ihv-trace-logging-overview"></a>IHV トレースログを使用したユーザーによるフィードバックの概要

このセクションのこのトピックでは、フィードバックツールを使用して送信されたユーザーによるフィードバック (UIF) レポートで、詳細な IHV トレースログを収集するために必要な手順の概要を示します。 フィードバックツールがログを収集するシナリオは2つあります。 最初のシナリオは、ユーザーがフィードバックを開始した時点でのシステムのスナップショットです。 この期間中、Windows は WMI 自動ロガーとその他のスナップショットデータを収集します。 2番目のシナリオでは、ユーザーが問題を再現します。 このフィードバック中に、Windows は詳細ログ記録を行い、ファイルサイズを大きくして、再現できる限り多くのデータをキャプチャする logger を開始します。 このセクションでは、これらのフィードバックシナリオごとに Ihv が期待することについて説明します。

このセクションの内容

- [ログ記録のシナリオ](logging-scenarios.md)
- [ユーザーが開始したフィードバック-標準モード](user-initiated-feedback-normal-mode.md)
- [ユーザーが開始したフィードバック-再現モード](user-initiated-feedback-repro-mode.md)
