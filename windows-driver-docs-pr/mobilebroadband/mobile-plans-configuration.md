---
title: Mobile のプランの構成
description: このトピックでは、Mobile プラン プログラムの構成手順について説明します。
ms.assetid: 95122BBB-0466-4130-9209-7EC6545DFD4D
keywords:
- Windows Mobile のプランの構成、モバイルのプランの構成モバイル演算子
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: a56ceca2d719f2813979c28b86b616b328f0425b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559672"
---
# <a name="mobile-plans-configuration"></a>Mobile のプランの構成

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

このトピックでは、Mobile の計画をサポートする Windows 接続されているデバイスの基盤を構築する方法を説明します。 Mobile プランにより、サービスの構成情報を提供するエクスペリエンスが適切にレンダリング Windows デバイスでどのように、最適なコンシューマーのエクスペリエンスもさせる、eSIM プロファイルを構成する方法も詳しく説明します。

## <a name="esim-profile-configuration-requirements"></a>esim 状プロファイル構成の要件

次の要件を満たす eSIM プロファイルを準備する必要があります。

- ESIM プロファイルでは、PIN ロックすることはできません。
- Esim 状プロファイルする必要があります、SM から削除できません-DP + サーバー プロファイルのダウンロードが正常に完了したことの確認を受信するまでです。 アクティブ化コードは、ダウンロードを前の試行が失敗した場合、同じプロファイルをダウンロードを再試行する再利用できます。 
- 「削除しないでください」または「は非アクティブ化できません」のポリシーの設定、eSIM プロファイルは必要ありません。
- アクティブ化コードがなど任意のプレフィックスを含めるいない必要があります"以下:"です。
- アクティブ化コードは、MO を直接フロー後すぐに使用できます。
- ESIM プロファイルからダウンロードできます直ちに SMDP + サーバー MO を直接フロー後。
- デバイスできますすぐにネットワークに接続、エンドユーザーは、esim 状のダウンロードし、アクティブ化した後。

Mobile のプランのユーザー エクスペリエンスがウォームの状態でデータ プランをアクティブにできることを意味する eSIM プロファイルが必要ですが最後に、リアルタイム eSIM プロファイルをダウンロードした後。

## <a name="service-configuration"></a>サービス構成

ESIM プロフィールの準備ができたら、Microsoft の構成サービスが通信事業者としてサポートするサービス プラットフォームを構成する必要があります。 このプロセスを開始するには、メールを送る[ DYNAMOpartnersup@microsoft.com ](mailto:swifipartnersup@microsoft.com)をオンボーディングするための次の情報。 

1.  ブランド名は、自社製品を使用したいです。
2.  ブランド ロゴです。 必要な解像度は次のとおりです。150 x 150、188 x 188、225 x 225、600 x 600、300 x 300、および 400 x 400 ピクセルです。 イメージは、フルブリード透過性なしでもあります。
3.  ソリューションがサポートされている国の一覧。
4.  MO 直接ポータル URI。
5.  通知 (実装で説明) URI。
6.  ICCID 範囲または Mobile 計画と関連付ける範囲。

次の図は、プランのモバイル アプリで商品情報とプロバイダーの説明 ページ (PDP) のレイアウトの例を示します。 "A"注釈に対応するブランド ロゴを送信して、"B"の注釈は、ブランド名に対応します。

<img src="images/dynamo_configuration_mo_page.png" alt="Mobile Plans mobile operator page - asset usage example" title="プランのモバイル携帯電話会社ページ - 資産の使用例" width="600" />