---
title: Mobile のプランのユース ケース
description: このトピックでは、モバイルの演算子を実装する基本的なユーザー ケースについて説明します。
ms.assetid: 24050B13-4A1A-466F-974B-40B34EDB16DC
keywords:
- Windows Mobile のプランのユーザーの場合、モバイルのプランの実装モバイル演算子
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8119bb90eb86a6849307020b60cfccab973f0983
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845575"
---
# <a name="mobile-plans-use-cases"></a>Mobile のプランのユース ケース

## <a name="overview"></a>概要

このトピックでは、モバイルのプランを持つモバイル オペレーターが可能にする最も一般的なユース ケースに関する詳細情報を提供します。 これがサポートされているケースの徹底的な一覧ではないことに注意してください。 可能性の高いソリューションの組み合わせを使用して、特定のユース ケースを達成できることになります。 さらに、シナリオを説明する Microsoft の担当者に連絡してください。

## <a name="install-an-esim-profile-on-a-windows-device"></a>Windows デバイスで、eSIM プロファイルをインストールします。

このセクションでは、通信事業者の実装をアクティブ化、ダウンロード、および Windows デバイスで、eSIM プロファイルをインストールする必要がありますについて説明します。 ネットワーク バックエンドと、ライセンス認証プロセスにかかる時間の特定の条件に基づいてプランのモバイル アプリに制御を返す方法の 1 つ以上を実装できます。

以下の操作を行ってください。

1. 実装、 [web ポータルのモバイル プラン](mobile-plans-web-portal.md#web-service-api-used-for-esim)します。
2. プランのモバイル アプリに戻すコントロールを提供する手段を実装します。
   1. [インライン プロファイル配信](mobile-plans-callback-notifications.md#inline-profile-delivery)します。 Esim 状プロファイルは、SM ですぐに利用可能な場合は、このコールバックを実装-DP + サーバーとデバイスに接続できる移動体通信ネットワークすぐにします。
   2. [非同期接続](mobile-plans-callback-notifications.md#asynchronous-connectivity)します。 Esim 状プロファイルは、SM ですぐに利用可能な場合は、このコールバックを実装-DP + サーバーが、デバイスが移動体通信ネットワークに接続する前に少し時間を待機する必要があります。
   3. **非同期のプロファイルのダウンロード**します。 Esim 状プロファイルは、SM で使用可能な場合は、このコールバックを実装-DP + サーバーの一定の時間と、デバイスが移動体通信ネットワークにすぐにアタッチできません。
3. [Esim 状のダウンロード エラーの処理](mobile-plans-eSIM-error-handling.md)します。 (省略可能)
4. 定義、[基本的なデバイス エクスペリエンス](mobile-plans-device-experience.md#basic-device-experience)します。
5. 提供[Mobile プラン サービスの構成](mobile-plans-service-configuration.md)情報。
6. [検証](mobile-plans-integration.md)実装します。
7. 商用[起動](mobile-plans-launch.md)します。

## <a name="add-balance-to-a-current-subscription"></a>現在のサブスクリプションに残高を追加します。

このセクションでは、現在のサブスクリプションに残高を追加するために必要な作業について説明します。 これは、プリペイド プランを販売している場合、または後払いサブスクリプションのインターネットのデータが不足すると、データ パッケージを販売する場合に便利です。

1. 実装、 [web ポータルの Mobile Operator](mobile-plans-web-portal.md)します。
2. 実装、[残高を追加する](mobile-plans-callback-notifications.md#adding-balance)Mobile プランに戻すコントロールを渡すことにします。
3. 実装、[デバイス エクスペリエンスを強化](mobile-plans-device-experience.md#enhanced-device-experience)します。
   1. 実装、[残高 API 取得](mobile-plans-device-experience.md#getbalance-api)します。
   2. 実装、[ウォール ガーデン](mobile-plans-device-experience.md#walled-garden)します。
4. 提供[Mobile プラン サービスの構成](mobile-plans-service-configuration.md)情報。
5. [検証](mobile-plans-integration.md)実装します。
6. 商用[起動](mobile-plans-launch.md)します。

## <a name="cancelling-a-transaction"></a>トランザクションをキャンセル

このセクションには、ユーザーが携帯電話会社の web ポータルでは、トランザクションが取り消されたときに、プランのモバイル アプリに通知するために使用するコントロールのコールバックがについて説明します。 これは、このトピックで前のすべてのシナリオに適用されます。

- 実装、 [Canceling 購買フロー](mobile-plans-callback-notifications.md#canceling-purchase-flow)コントロール。

## <a name="activate-a-warm-sim-in-a-windows-device"></a>ウォーム SIM で Windows デバイスをアクティブ化します。

このセクションでは、通信事業者の実装、ウォーム SIM プロファイルを Windows デバイスでアクティブ化する必要がありますについて説明します。

以下の操作を行ってください。

1. 実装、 [web ポータルの Mobile Operator](mobile-plans-web-portal.md#web-service-api-used-for-a-physical-sim)します。
2. 実装、[残高を追加する](mobile-plans-callback-notifications.md#adding-balance)Mobile プランに戻すコントロールを渡すことにします。
3. 実装、[デバイス エクスペリエンスを強化](mobile-plans-device-experience.md#enhanced-device-experience)します。
   1. 実装、[残高 API 取得](mobile-plans-device-experience.md#getbalance-api)します。
   2. 実装、[ウォール ガーデン](mobile-plans-device-experience.md#walled-garden)します。
4. 提供[Mobile プラン サービスの構成](mobile-plans-service-configuration.md)情報。
5. [検証](mobile-plans-integration.md)実装します。
6. 商用[起動](mobile-plans-launch.md)します。