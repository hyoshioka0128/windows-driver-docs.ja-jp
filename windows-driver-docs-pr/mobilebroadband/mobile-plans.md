---
title: モバイル通信プラン
description: モバイル通信プラン
ms.assetid: AA432EAE-A89B-4C4C-9539-BC2763091055
keywords:
- 携帯電話会社の Windows Mobile の計画
ms.author: windowsdriverdev
ms.date: 03/25/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 7b8ba7e497ee9ede100e110fbfe0b76a299c4093
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845531"
---
# <a name="mobile-plans"></a>モバイル通信プラン

## <a name="introduction"></a>概要

Mobile プランは、Windows 10、バージョン 1803 でプログラムし、エンドユーザーにプランを販売するには、携帯電話会社 (MOs) やその他のサービス プロバイダーを可能な以降。

Mobile のプランには、次を実行するエンドユーザーができるように。

- インストールし、eSIM プロファイルをアクティブ化します。
- 前払い (PAYG) または後払いプランのいずれかで携帯電話会社のサブスクリプションでのデバイスを有効にします。
- サブスクリプションを上のデータとのみ使用可能な接続がモバイル接続します。

## <a name="definition-of-terms"></a>用語の定義

| 項目 | 説明 |
| --- | --- |
| Contoso の携帯電話 | 以下のトピックで説明のために使用される架空モバイル演算子。 |
| COSA データベース | 国および演算子の設定の資産。 これは、Windows デバイスで使用される通信事業者の接続設定を含むデータベースです。 COSA に関する詳細については、[COSA 概要](cosa-overview.md)を参照してください。 |
| モバイル通信プラン | このプロジェクトの名前。 |
| プランのモバイル アプリ | Windows 10 デバイスでモバイルのプランを有効にする Microsoft アプリ。 |
| Mobile プラン サービス | プランのモバイル ソリューションをできるようにするクラウド サービスです。 |
| RP | 1 秒あたりの要求。 |

## <a name="project-overview"></a>プロジェクトの概要

プランのモバイル プロジェクトの統合は、それぞれがの 4 つのステージで構成されます[高度なタスク](mobile-plans-appendix.md#high-level-integration-schedule)します。 一部の高度なタスクは、Microsoft が携帯電話会社と連携して動作を共同作業がモバイル オペレーター用です。

| ステージ | 説明 |
| --- | --- |
| **実行可能性** | 携帯電話会社 Mobile 計画ソリューションを評価するには、このドキュメントでは、ダイジェストとなるおよび必要に応じて、Microsoft の担当者の質問をに達するとします。 |
| **実装** | 携帯電話会社は、そのユーザーの場合と要求 Mobile プランの構成と必要に応じて、Windows の構成に従って、ソリューションを開発しています。 |
| **統合** | 携帯電話会社は、エンド ツー エンドの検証を実行するモバイルのプランで有効です。 |
| **起動** | 携帯電話会社が販売されているモバイル プランを市場に起動されます。 |

## <a name="functional-overview"></a>機能の概要

次の図は、Windows 10 デバイスを使用した方法 Mobile プランの異なるサービスやソリューションを正常にサブスクリプションをアクティベートして、eSIM プロファイルのインストールとの対話の概要を示します。

次の表では、図の各コンポーネントについて説明します。

| コンポーネント | 説明 |
| --- | --- |
| Windows 10 デバイス | ESIM 対応"常に接続されている PC"最新のバージョンの Windows 10 を実行します。 |
| Microsoft のモバイル サービスを計画します。 | 月の web ポータルなどの携帯電話会社情報を提供する担当サービス エンドポイント URL とビジュアル アセットと、Windows 10 デバイスです。 |
| モバイルのプランの Web API および Web ポータル | 通信事業者ネットワーク、web サービス API と Windows 10 デバイスをモバイル プランにアクセスを許可する web ポータルをホストする役割があるエンドポイントが発生します。 |
| SM-DP + サーバー | 作成、生成、および携帯電話会社に属している eSIM プロファイルの管理を担当します。 |

<img src="images/mobile_plans_functional_overview.png" alt="Mobile Plans functional overview" title="Mobile の計画機能の概要" width="400" />

前の図の一般的な機能のフローは次のとおりです。

1. プランのモバイル アプリでは、Windows 10 デバイス上で起動し、Mobile プラン サービスからの基本的な機能の情報を取得します。
   - プランのモバイル アプリは、月に固有の情報を取得するプランのモバイル サービスには、に到達します。
2. プランのモバイル アプリでは、MO Web ポータルを起動し、MO ポータルに関連するパラメーターを渡します。
3. 携帯電話会社、SM から eSIM プロファイルを要求する-DP + サーバー。 Esim 状のアクティブ化コードは、プランのモバイル携帯電話会社の web ポータルに返されます。
4. コントロールがプランのモバイル アプリに返されると、Windows 10 デバイスで、esim 状のアクティブ化コードは、Windows デバイスに提供されます。
5. Windows 10 デバイスのアクティブ化コードを使用し、SM に接続-DP + server esim 状のプロファイルを取得します。 Esim 状のプロファイルがインストールされ、Windows 10 デバイスでアクティブ化されるようになりました。
6. Windows 10 デバイスは、通信事業者ネットワークに接続されます。

Windows では、モバイルのプランの全体的なエクスペリエンスを使用するのにクライアントとして、プランのモバイル アプリを使用します。 このアプリケーションは、MO Web ポータルにアクセスし、その対話を処理します。 また、アクティブ化コードが返されると、プランのモバイル アプリはダウンロード、インストール、および eSIM プロファイルをアクティブ化する責任を負います。

## <a name="get-started"></a>作業開始

Mobile の計画を開始するまでの経験、プロジェクトの実装について説明する、Microsoft の担当者に到達してください。 ソリューションの技術的な詳細を理解するためのガイドは、次の手順に従います。

1. [携帯電話会社のユース ケース](mobile-plans-use-cases.md)
2. [統合](mobile-plans-integration.md)
3. [起動](mobile-plans-launch.md)

Mobile の計画に関する追加情報は次のトピックを参照してください。

- [付録](mobile-plans-appendix.md)