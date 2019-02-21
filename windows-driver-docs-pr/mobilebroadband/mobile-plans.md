---
title: モバイルの計画
description: モバイルの計画
ms.assetid: AA432EAE-A89B-4C4C-9539-BC2763091055
keywords:
- 携帯電話会社の Windows Mobile の計画
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: e954b7a95e53fa41543a716085fabe0347334172
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532089"
---
# <a name="mobile-plans"></a>モバイルの計画

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

## <a name="introduction"></a>概要

Mobile プランは、Windows 10、バージョン 1803 でプログラムし、エンドユーザーにプランを販売するには、携帯電話会社 (MOs) やその他のサービス プロバイダーを可能な以降。 Mobile の計画前のデータ マーケットプ レース アプリケーションの新しい名前を指定し、個別または競合するプログラムではありません。

Mobile のプランには、次を実行するエンドユーザーができるように。

- インストールし、eSIM プロファイルをアクティブ化します。
- 前払い (PAYG) または後払いプランのいずれかで携帯電話会社のサブスクリプションでのデバイスを有効にします。
- 前払いサブスクリプションを上のデータとのみ使用可能な接続がモバイル接続します。

## <a name="definition-of-terms"></a>用語の定義

| 用語 | 説明 |
| --- | --- |
| Contoso の携帯電話 | 以下のトピックで説明のために使用される架空モバイル演算子。 |
| COSA データベース | 国および演算子の設定の資産。 これは、Windows デバイスで使用される通信事業者の接続設定を含むデータベースです。 COSA に関する詳細については、次を参照してください。 [COSA 概要](cosa-overview.md)します。 |
| モバイルの計画 | このプロジェクトの名前。 |   
| プランのモバイル アプリ | Mobile の計画、以前の有料の Wi-fi および移動体通信 (PWC) アプリを有効にする Microsoft アプリ。 |
| PAYG | 従量課金制 |
| RP | 1 秒あたりの要求 |

## <a name="project-overview"></a>プロジェクトの概要

プランのモバイル プロジェクトの統合は、高度なタスクを持つ 4 つのステージで構成されます。 一部の高度なタスクは、Microsoft が携帯電話会社と連携して動作を共同作業がモバイル オペレーター用です。 次の図は、プランのモバイル プロジェクトの 4 つの段階を示しています。

<img src="images/dynamo_project_overview.png" alt="Mobile Plans project overview" title="プランのモバイル プロジェクトの概要" width="600" />

## <a name="functional-overview"></a>機能の概要

次の図は、Windows 10 デバイスを使用した方法 Mobile プランの異なるサービスやソリューションを正常にサブスクリプションをアクティベートして、eSIM プロファイルのインストールとの対話の概要を示します。

次の表では、図の各コンポーネントについて説明します。

| Component | 説明 |
| --- | --- |
| Windows 10 デバイス | ESIM 対応"常に接続されている PC"最新のバージョンの Windows 10 を実行します。 |
| Microsoft のモバイル サービスを計画します。 | サービス エンドポイントが電話番号の参照と、MO などの携帯電話会社情報を提供する web ポータルの URL とビジュアルの解決を担当する Windows 10 デバイスの資産。 |
| モバイルのプランの Web API および Web ポータル | 通信事業者ネットワーク、web サービス API と Windows 10 デバイスをモバイル プランにアクセスを許可する web ポータルをホストする役割があるエンドポイントが発生します。 |
| SMDP + サーバー | 作成、生成、および携帯電話会社に属している eSIM プロファイルの管理を担当します。 |

<img src="images/dynamo_functional_overview.png" alt="Mobile Plans functional overview" title="Mobile の計画機能の概要" width="600" />

前の図の一般的な機能のフローは次のとおりです。

1. プランのモバイル アプリ、Windows 10 デバイスで実行されているモバイル プラン サービスの電話番号の参照を解決します。
2. プランのモバイル アプリは、月に固有の情報を取得するプランのモバイル サービスには、に到達します。
3. プランのモバイル アプリでは、月の web ポータルを起動し、MO ポータルに関連するパラメーターを渡します。
4. 携帯電話会社、SM から eSIM プロファイルを要求する-DP + サーバー。 Esim 状のアクティブ化コードは、携帯電話会社のモバイル プラン サーバーに返されます。
5. コントロールがプランのモバイル アプリに返されると、Windows 10 デバイスで、esim 状のアクティブ化コードは、Windows デバイスに提供されます。
6. Windows 10 デバイスのアクティブ化コードを使用し、SM に接続-DP + server esim 状のプロファイルを取得します。 Esim 状のプロファイルがインストールされ、Windows 10 デバイスでアクティブ化されるようになりました。
7. Windows 10 デバイスは、通信事業者ネットワークに接続されます。

Windows では、モバイルのプランの全体的なエクスペリエンスを使用するのにクライアントとして、プランのモバイル アプリを使用します。 このアプリケーションは、MO Web ポータルにアクセスし、その対話を処理します。 また、アクティブ化コードが返されると、プランのモバイル アプリはダウンロード、インストール、および eSIM プロファイルをアクティブ化する責任を負います。

## <a name="get-started"></a>はじめに

後払い Mobile 計画を開始するエクスペリエンスで、これらの手順に従います。

1. [構成](mobile-plans-configuration.md)
2. [実装](mobile-plans-implementation.md)
3. [統合](mobile-plans-integration.md)
4. [起動](mobile-plans-launch.md)

Mobile の計画に関する追加情報は次のトピックを参照してください。

- [前払いエクスペリエンス](mobile-plans-prepaid-experience.md)
- [付録](mobile-plans-appendix.md)