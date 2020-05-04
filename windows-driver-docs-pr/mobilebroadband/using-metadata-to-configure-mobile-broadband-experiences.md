---
title: メタデータを使用したモバイル ブロードバンド エクスペリエンスの構成の概要
description: メタデータを使用したモバイル ブロードバンド エクスペリエンスの構成の概要
ms.assetid: d3ceab6e-550f-4852-8ee0-4a261c238434
ms.date: 07/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2d6ec527e943738f773826a8a4af4e235a5500fa
ms.sourcegitcommit: 9b791a85c471f0d7707a4a28a2ca273713b7993e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82558849"
---
# <a name="overview-of-using-metadata-to-configure-mobile-broadband-experiences"></a>メタデータを使用したモバイル ブロードバンド エクスペリエンスの構成の概要

> [!IMPORTANT] 
> Windows 10 バージョン1703以降では、APN データベースは COSA という新しい形式に置き換えられています。 Windows 8、Windows 8.1、および windows 10 1703 より前のバージョンの windows 10 では、Windows 10 バージョン1703以降では、引き続き APN データベースが使用されます。 COSA の詳細については、 [Cosa の概要](cosa-overview.md)に関するトピックを参照してください。
>
> Windows 10 バージョン1803以降では、MBAE アプリのエクスペリエンスは、UWP アプリの MO 概要に置き換えられています。 UWP アプリの詳細については、「 [uwp モバイルブロードバンドアプリの概要](uwp-mobile-broadband-apps.md)」を参照してください。

メタデータを提供して、Windows 8、Windows 8.1、および Windows 10 mobile のブロードバンドアプリケーションエクスペリエンスのさまざまな側面をカスタマイズできます。 これには、オペレーターのブランド化による Windows 接続マネージャーのカスタマイズ、モバイルブロードバンドアプリと Windows 接続マネージャーの統合、Windows APN データベースの更新情報の提供、および PC をプロビジョニングするためのデータの提供が含まれます。 Windows 8、Windows 8.1、Windows 10 には、次の3つのソースのメタデータを使用できます。

-   **WINDOWS APN データベース**Windows APN データベースには、オペレーターのネットワークに初めて接続するために必要な事前にプロビジョニングされたデータが含まれています。 データベースは Windows 8、Windows 8.1、および Windows 10 の一部であり、更新プログラムの Windows の概要を使用して更新されます。 Windows APN データベースは、常に PC で使用できます。 COSA と APN データベースの詳細については、 [cosa/apn データベース](cosa-apn-database.md)に関する情報を参照してください。

-   **サービスメタデータ**サブスクリプションの購入とオペレーターのブランド化に必要な情報。 この情報は、サービスメタデータパッケージの一部として提供します。 このファイルは Windows メタデータおよびインターネットサービス (WMIS) に保存され、使用可能なインターネット接続を使用してモバイルブロードバンドデバイスが検出された後にダウンロードされます。 このメタデータは、OEM によって PC にプレインストールすることもできますが、ダウンロードしたパッケージは、Windows デベロッパーセンターのハードウェアの [開発者] セクションからプレインストールする必要があります。 サービスメタデータの詳細については、「[サービスメタデータ](service-metadata.md)」を参照してください。

-   **アカウントプロビジョニングメタデータ**サブスクリプションの購入後に生成される情報 (Wi-fi 資格情報やプラン情報など)。 このメタデータは、支払いの検証後に Windows に提供され、プロビジョニング更新メカニズムを使用して更新できます。 アカウントプロビジョニングメタデータの詳細については、「[アカウントのプロビジョニング](account-provisioning.md)」を参照してください。

次の図は、さまざまなメタデータソースがどのように関連しており、どのように処理されるかを示しています。 サービスメタデータは、Windows APN データベースの情報よりも優先されます。

![これは、モバイルブロードバンドの概要です。](images/mbae-sxs-overview.jpg)

の概要このセクションのリンクを使用して、さまざまな種類のモバイルブロードバンドメタデータの詳細を確認してください。

-   [アカウント プロビジョニング](account-provisioning.md)

-   [COSA/APN データベース](cosa-apn-database.md)

-   [サービスメタデータ](service-metadata.md)
