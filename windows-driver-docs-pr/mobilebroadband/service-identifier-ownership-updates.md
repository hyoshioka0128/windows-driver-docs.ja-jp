---
title: サービス識別子の所有権の更新
description: サービス識別子の所有権の更新
ms.assetid: 6cb03631-def6-44d4-a73a-0e6124e3b1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaf44eb94498aba5efd2957c133d9db84073a015
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323704"
---
# <a name="service-identifier-ownership-updates"></a>サービス識別子の所有権の更新

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


サービス識別子は、モバイルブロードバンドデバイス (GSM の場合は SIM カード、CDMA の場合は modem) でエンコードされた一連のフィールドであり、デバイスを一意に識別するために使用されます。 サービス識別子は、Windows 8、Windows 8.1、および Windows 10 で、そのデバイスのサービスメタデータパッケージをダウンロードするために使用されます。 サービスメタデータパッケージを作成する前に、サービス id を Windows デベロッパーセンターハードウェアダッシュボードに登録する必要があります。 新しいサービス識別子の登録の詳細については、「[開発者ガイド」を](developer-guide-for-creating-service-metadata.md)参照してください。

テクノロジによっては、サービス識別子は次のように構成されます。

-   GSM

    -   **プロバイダー ID**モバイルの国コードとモバイルネットワークコードの組み合わせ (5 桁または6桁の数字)。

    -   **プロバイダー名**ファームウェアのプロビジョニング時にデバイスにフラッシュされた名前。

-   CDMA

    -   **SID**CDMA ネットワークのシステム識別子 (SID)。

    -   **プロバイダー名**ファームウェアのプロビジョニング時にデバイスにフラッシュされた名前。

IMSI の所有権が変更された場合、新しいオペレーターは、次の情報を含む電子メールを sysdev@microsoft.com に送信する必要があります。

-   Windows デベロッパーセンターハードウェアダッシュボードの登録プロセス中にオペレーターが使用する組織名

-   IMSI を所有していた古い携帯電話事業者の名前

-   所有権の変更によって影響を受けた GSM プロバイダー Id の一覧

要求を受け取った24時間の受信確認メールを受信する必要があります。 ただし、要求の処理には最大5営業日かかることがあります。 競合がある場合は、追加情報を求める電子メールをお送りします。

 

 





