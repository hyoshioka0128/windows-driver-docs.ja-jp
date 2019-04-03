---
title: モバイルのプランの統合
description: このトピックでは、Mobile プラン プログラムの統合手順を説明します。
ms.assetid: F818B69D-DFA3-4296-B420-43F59D370E3C
keywords:
- Windows Mobile プランの統合、Mobile のプランの統合モバイル演算子
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3c7fb09cf1195713a35843206dd5557bab689797
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845535"
---
# <a name="mobile-plans-integration"></a>モバイルのプランの統合

## <a name="overview"></a>概要

このトピックでは、統合し、プランのモバイル ソリューションの通信事業者の実装を検証する手順が必要なについて説明します。

## <a name="mobile-plans-service-environments"></a>プランの Mobile service の環境

2 つサービスの環境をモバイル プラン、*ステージング*と*運用*します。 統合と検証が実行される、*ステージング*環境では中、*運用*環境は、商用の起動でのみ使用します。

## <a name="validation"></a>［確認］

このセクションには、テストと検証の統合のフェーズに移動する準備ができていることを確認する必要がありますがについて説明します。

### <a name="mobile-operator-web-portal"></a>Web ポータルのモバイル演算子

定義した 50 個のエンド ツー エンド ユーザー ケースを実行できることを検証します。 以下に例を示します。

- Esim 状、プロファイルをインストールします。
- ウォーム SIM を有効にします。
- サブスクリプションに残高を追加します。
- トランザクションを中止しています。

### <a name="walled-garden"></a>高いガーデン

ユーザーには、残高がない、Walled Garden のサイトで定義されているをユーザーがアクセスできることを確認します[Walled Garden](mobile-plans-device-experience.md#walled-garden)します。

### <a name="getting-balance"></a>残高を取得します。

1. ユーザーは、Walled Garden 状態が、返される残高はゼロでなければなりません。
2. ユーザーは、データを消費するよう、残高が返されますが残りのデータを反映するようにデクリメントする必要があります。
3. 後に割り当てられた時間経過として、 `Create Order` API が呼び出された、残り時間を反映するように、残りの期間をデクリメントする必要があります。

### <a name="test-with-expired-mtls-certificate"></a>MTLS の有効期限が切れた証明書を使用してテストします。

1. MTLS 証明書がない、MO Api を検証します。 予期される状態:401 許可されていません。
2. 有効期限が切れた MTLS 証明書を検証します。 予期される状態:401 許可されていません。

### <a name="getbalance-negative-tests"></a>GetBalance ネガティブ テスト

1. 無効な SIM で検証します。 予期される状態:404 not Found です。
2. 不明な場所または不適切な場所の文字列/数値を検証します。 予期される状態:400 (bad Request)。
3. 負の数値としてフィルターの制限を使用して検証し、INT の制限を超える 予期される状態:400-正しくない要求。 フィルターの制限 (整数) ステータス 200 OK が必要です。
4. 呼び出しを検証`GetBalance`ことがなく、*場所*(または空の場所)、 *fieldTemplate*、*制限*、およびパラメーターの多くの組み合わせ。 予期される状態:不適切なパラメーターの値の 400 (bad Request) をします。 OK ステータス 200 – が必要です。

### <a name="getbalance-api-load-test"></a>GetBalance API のロード テスト

前に、 `GetBalance` API が運用環境で有効になっている、予想される負荷を処理できるかどうかに表示するプランのモバイル サービスと通信事業者のサービスの両方をテストしてください。 携帯電話会社は、ロード テストの実行が必要です。 経過するとモバイルのプランはロード テストを実行します。 携帯電話会社は、ロード テストで使用される一時的に 1000 いる Iccid の一覧を指定する必要があります。

このテスト構成は、10,000 Sim の予想されるトラフィックから生成されます。 ピーク RPS は 3 回このトラフィック投影に基づいて計算されます。

- ロード テストは、25 のテスト エージェントから実行されます。
- ロード テストが実行されます。
  - 3 RPS (ピーク時) にさまざまなユーザー (#ICCIDs) 1000 と 1 時間です。
- 負荷分散は、クロス Api は次のようになります。

| API | 負荷分散 | 予想される RPS | ピーク時の RPS |
| --- | --- | --- | --- |
| GetBalance | 96% | 1 | 3 |

テストの実行中に予期される成功率は次のとおりです。99.9%. この成功率を実現するためには、MO API が Mobile プランの運用環境サービスで有効にする準備ができます。