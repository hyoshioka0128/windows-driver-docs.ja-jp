---
title: IHV トレース ログによるユーザーが開始したフィードバック
description: このセクションでは、このトピックでは、フィードバック ツールを使用して送信されたユーザーが開始したフィードバック (し) レポートの中に詳細の IHV トレース ログを収集するために必要な手順を説明します。
ms.assetid: BDD02AA2-A771-4AC1-B9D2-E9E8FA073B7A
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 28e4767318dff87b7f98c3db24d783f72ac7960c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362494"
---
# <a name="user-initiated-feedback-with-ihv-trace-logging"></a>IHV トレース ログによるユーザーが開始したフィードバック

このセクションでは、このトピックでは、フィードバック ツールを使用して送信されたユーザーが開始したフィードバック (し) レポートの中に詳細の IHV トレース ログを収集するために必要な手順を説明します。 フィードバック ツールがログを収集する 2 つの独立したシナリオがあります。 最初のシナリオでは、ユーザーがフィードバックを開始する時に、システムのスナップショットです。 この期間中は、Windows は、WMI の自動ロガーとその他のいくつかのスナップショット データを収集します。 2 番目のシナリオでは、ユーザーの問題を再現する必要があります。 このフィードバックは、中には、Windows は、詳細ログ記録と大きなファイル サイズの再現コードでは、できるだけ多くのデータをキャプチャするロガーを開始します。 このセクションでは、ihv 向けの期待するは、各フィードバック シナリオについて説明します。

このセクションの内容

- [ログ記録シナリオ](logging-scenarios.md)
- [ユーザーによって開始されたフィードバック - 標準モード](user-initiated-feedback-normal-mode.md)
- [ユーザーが開始したフィードバックの再現コード モード](user-initiated-feedback-repro-mode.md)
