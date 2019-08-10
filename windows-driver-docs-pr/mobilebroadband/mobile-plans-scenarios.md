---
title: モバイル通信プランのシナリオ
description: このトピックでは、モバイルオペレーターが実装できる基本的なエンドユーザー向けシナリオについて説明します。
ms.assetid: 24050B13-4A1A-466F-974B-40B34EDB16DC
keywords:
- Windows Mobile プランのシナリオ, モバイルプランの実装モバイルオペレーター
ms.date: 05/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1a89a4590872b0fa2f856148b6c788cc6ae49179
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948107"
---
# <a name="mobile-plans-scenarios"></a>モバイル通信プランのシナリオ

## <a name="overview"></a>概要

このトピックでは、モバイルオペレーターがモバイルプランで有効にする最も一般的なシナリオに関するガイダンスを提供します。 これは、サポートされるシナリオの完全な一覧ではないことに注意してください。 ソリューションを組み合わせることによって、特定のユースケースを実現できる可能性があります。 要件について詳しくは、Microsoft の担当者にお問い合わせください。

## <a name="install-an-esim-profile-on-a-windows-10-device"></a>Windows 10 デバイスに eSIM プロファイルをインストールする

このセクションでは、Windows 10 デバイスで eSIM プロファイルをダウンロード、インストール、およびアクティブ化するために携帯電話事業者が行う必要がある手順について説明します。 携帯電話会社の eSIM プラットフォームとネットワークバックエンドの constrainsts に応じて、アクティブ化フローの最後にプロファイルとネットワーク接続を実現するために使用される方法が複数あります。

1. サインインとアクティブ化の手順を通じてユーザーを受け取る[携帯電話会社の web ポータル](mobile-plans-web-portal.md#web-portal-interface-for-esim-enabled-devices)を開発します。
2. サポートされているコールバックメソッドの1つを実装して、eSIM プロファイルをダウンロードするために制御をモバイルプランアプリに戻します。
   1. [インラインプロファイルのダウンロードと接続](mobile-plans-callback-notifications.md#inline-profile-download-and-connectivity)-このコールバックメソッドは、プロファイルが既に SM-DP + サーバーによって解放されている場合に使用する必要があり、プロファイルによってデバイスは、プロファイルの直後に携帯ネットワークに登録できるようになります。認証. このメソッドは、同じエンドユーザーフローの一部として、プロファイルの配信とネットワーク接続を有効にします。
   2. [非同期接続](mobile-plans-callback-notifications.md#asynchronous-connectivity)。 このコールバックメソッドは、eSIM プロファイルが既に SM DP + サーバーによってリリースされている場合に使用する必要がありますが、デバイスは、携帯ネットワークに登録する前にしばらく待つ必要があります。
   3. [プロファイルのダウンロードが遅れ](mobile-plans-callback-notifications.md#delayed-esim-profile-download-and-activation)ています。 このコールバックメソッドは、プロファイルが SM DP + サーバーによって解放されない場合に使用する必要があり、一定期間後にのみダウンロードできます。 プロファイルをダウンロードしてインストールすると、デバイスは携帯ネットワークに登録できることが想定されます。
3. [プロファイルのダウンロードエラーを適切に処理](mobile-plans-eSIM-error-handling.md)します。
4. ユーザーがアカウントを管理および管理するための[基本的なアカウント管理エクスペリエンス](mobile-plans-account-management.md#basic-account-management-experience)を実装します。

## <a name="activate-a-warm-sim-in-a-windows-device"></a>Windows デバイスでのウォーム SIM のアクティブ化

このセクションでは、ユーザーが Windows デバイスでウォーム phsycial SIM をアクティブ化できるようにする手順について説明します。 "ウォーム" という用語は、preactivated されているが、携帯電話会社に接続されていても、アクティブなサブスクリプションに関連付けられていない SIM を指します。

1. サインインとアクティブ化の手順を通じてユーザーを操作する[モバイルオペレーター web ポータル](mobile-plans-web-portal.md#web-portal-interface-for-physical-sims)を実装します。
2. [バランスを追加](mobile-plans-callback-notifications.md#adding-balance)するためのコールバックメソッドを実装します。
3. 強化された[アカウント管理エクスペリエンス](mobile-plans-account-management.md#enhanced-account-management-experience)を実装します。
   1. [Getbalance メソッド](mobile-plans-account-management.md#getbalance-api)を MOBILE operator API の一部として実装します。
   2. [Walled ガーデン](mobile-plans-walled-garden.md)を実装すると、ユーザーがアクティブな残高を持っていなくても、携帯電話会社の web ポータルに移動できるようになります。

## <a name="add-balance-to-a-current-subscription"></a>現在のサブスクリプションに残高を追加する

このセクションでは、既存の顧客サブスクリプションに残高を追加する手順について説明します。 invovled を参照してください。 これは、携帯電話会社が前払いデータプランを販売しているときに、残高が topped になる必要がある場合に便利です。

1. [携帯電話会社の web ポータル](mobile-plans-web-portal.md)を開発します。
2. [バランスを追加](mobile-plans-callback-notifications.md#adding-balance)するためのコールバックメソッドを実装します。
3. 強化された[アカウント管理エクスペリエンス](mobile-plans-account-management.md#enhanced-account-management-experience)を実装します。
   1. [Getbalance メソッド](mobile-plans-account-management.md#getbalance-api)をモバイルオペレーター API の一部として実装し、ユーザーのバランスを Windows ネットワークフライアウトに表示できるようにします。
   2. [Walled ガーデン](mobile-plans-walled-garden.md)を実装すると、ユーザーは、残高が残っていなくても、携帯電話会社の web ポータルに移動できるようになります。

## <a name="cancelling-a-transaction"></a>トランザクションを取り消す

このセクションでは、ユーザーがモバイルオペレーター web ポータルを閲覧しているときにトランザクションがキャンセルされた場合に、モバイルプランアプリに通知するために使用されるコールバックメソッドについて説明します。 これは、このトピックの前のすべてのシナリオに適用されます。

- [購入フローを取り消す](mobile-plans-callback-notifications.md#canceling-purchase-flow)ためのコールバックメソッドを実装します。
