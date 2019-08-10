---
title: モバイルプランサービスの構成
description: このトピックでは、モバイルプランプログラムの構成手順について説明します。
ms.assetid: 95122BBB-0466-4130-9209-7EC6545DFD4D
keywords:
- Windows Mobile プランの構成、モバイルプランの構成モバイルオペレーター
ms.date: 02/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: fe89966e0ea73d60ea20ce7057d495304ce57d7c
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948036"
---
# <a name="mobile-plans-service-configuration"></a>モバイルプランサービスの構成

このトピックでは、モバイルプランをサポートする Windows 接続デバイスで基礎を構築する方法について説明します。 ここでは、最適なコンシューマーエクスペリエンスを保証するために eSIM プロファイルを構成する方法と、モバイルプランのエクスペリエンスが Windows デバイスで適切にレンダリングされるようにするためのサービス構成情報を提供する方法について説明します。

## <a name="esim-profile-configuration-requirements"></a>eSIM プロファイルの構成要件

次の要件を満たす eSIM プロファイルを準備する必要があります。

- ESIM プロファイルを固定することはできません。
- プロファイルのダウンロードが正常に完了したことを確認するメッセージが表示されるまで、SM DP + サーバーから eSIM プロファイルを削除することはできません。 アクティブ化コードを再利用して、前回のダウンロードの試行が失敗したときに同じプロファイルのダウンロードを再試行することができます。
- ESIM プロファイルには、"削除しない" ポリシーまたは "非アクティブ化しない" ポリシーを設定することはできません。
- アクティベーションコードには、"LPA:" などのプレフィックスを含めることはできません。
- アクティブ化コードは、MO ダイレクトフローの直後に使用できます。
- アクティベーションコードには、"確認コード" は必要ありません。

### <a name="esim-profile-testing"></a>eSIM プロファイルのテスト

携帯電話会社が検証を実行して、その eSIM プロファイルを異なる Windows デバイスにインストールできることが前提となります。 そのためには、いくつかの eSIM 対応デバイスをソース化し、Windows 設定アプリを使用してプロファイルをダウンロード、インストール、およびアクティブ化することをお勧めします。

## <a name="service-configuration"></a>サービス構成

Mobile plan サービスは、携帯電話事業者をサポートするためにいくつかの構成情報を取り込む必要があります。 構成プロセスを開始するには、[モバイルプランの実装サポート](mailto:mpimplementation@microsoft.com)に電子メールを送信してください。

### <a name="minimum-configuration-information"></a>最小構成情報

1. 製品に対して使用するブランド名。
2. ブランドロゴ。 必要な解像度は300x300 ピクセルです。 画像は、透明度のない完全な裁ち落としでもある必要があります。
3. ソリューションがサポートされている国の一覧。 [ISO 3166 コード](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)を使用してリストを作成してください (コンマ区切り)。
4. MO ダイレクトポータルの URI (ローカライズはサポートされていません)。 これは*https*アドレスにする必要があります。 ポート番号はサポートされていません。
5. 通知 URI。 これは、Javascript のコールバック ([コールバック通知](mobile-plans-callback-notifications.md)) が実行されるホストアドレスです。 これは*https*アドレスにする必要があります。 ポート番号はサポートされていません。
6. *モバイルプラン*に関連付ける ICCID の範囲または範囲。

次の図は、モバイルプランアプリの*standard ゲートウェイページ*の例を示しています。 "A" 注釈は、送信するブランドロゴに対応し、"B" 注釈はブランド名に対応します。

<img src="images/mobile_plans_configuration_mo_page.png" alt="Mobile Plans mobile operator page - asset usage example" title="モバイルプランの携帯電話会社のページ-資産の使用例" width="600" />
