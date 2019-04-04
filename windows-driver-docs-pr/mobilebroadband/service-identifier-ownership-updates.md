---
title: サービスの識別子の所有権の更新プログラム
description: サービスの識別子の所有権の更新プログラム
ms.assetid: 6cb03631-def6-44d4-a73a-0e6124e3b1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaf44eb94498aba5efd2957c133d9db84073a015
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561052"
---
# <a name="service-identifier-ownership-updates"></a>サービスの識別子の所有権の更新プログラム

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


サービスの識別子では、(GSM の SIM カード) とモデムの CDMA モバイル ブロード バンドのデバイスでエンコードされ、デバイスを一意に識別するために使用されるフィールドのセットです。 サービスの識別子は、そのデバイスのサービス メタデータ パッケージをダウンロードする Windows 8、Windows 8.1、および Windows 10 で使用されます。 サービス メタデータ パッケージを作成する前に Windows デベロッパー センター ハードウェア ダッシュ ボードで、サービスの id を登録する必要があります。 新しいサービス id を登録する方法の詳細については、[サービス メタデータを作成するための開発者ガイド](developer-guide-for-creating-service-metadata.md)を参照してください。

サービスの識別子に、テクノロジによって、次の構成できます。

-   GSM

    -   **プロバイダー ID**モバイルの国コードとモバイル ネットワーク コード、5、6 桁の数字の組み合わせ。

    -   **プロバイダー名**ファームウェアがプロビジョニングされるときに、名前がデバイスにアップデートします。

-   CDMA

    -   **SID** CDMA ネットワークのシステム識別子 (SID)。

    -   **プロバイダー名**ファームウェアがプロビジョニングされるときに、名前がデバイスにアップデートします。

新しいオペレーターが電子メールを送信する必要があります、IMSI の所有権が変更された場合sysdev@microsoft.com次の情報を使用します。

-   Windows デベロッパー センター ハードウェア ダッシュ ボードの登録プロセス中に演算子によって使用される組織名

-   IMSI、所有している古い通信事業者の名前

-   所有権の変更によって影響を受ける GSM プロバイダー Id の一覧

要求を受信した 24 時間で、受信確認の電子メールを受信する必要があります。 ただし、要求を処理する最大 5 営業日かかる可能性があります。 競合がある場合お知らせする追加情報を求める電子メール。

 

 





