---
title: モバイル ブロード バンド エクスペリエンスを構成するメタデータの使用の概要
description: モバイル ブロード バンド エクスペリエンスを構成するメタデータの使用の概要
ms.assetid: d3ceab6e-550f-4852-8ee0-4a261c238434
ms.date: 07/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: add18828a06b1ff69f394d19cc337edc58abab7d
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608553"
---
# <a name="overview-of-using-metadata-to-configure-mobile-broadband-experiences"></a>モバイル ブロード バンド エクスペリエンスを構成するメタデータの使用の概要

> [!IMPORTANT] 
> APN データベースは Windows 10 バージョン 1703 以降 COSA と呼ばれる新しい形式に置換されます。 Windows 8、Windows 8.1、およびバージョンの Windows 10 1703 は Windows 10 は APN データベースの使用を続行する前に、バージョン 1703 以降は COSA を使用します。 COSA の詳細については、次を参照してください。 [COSA 概要](cosa-overview.md)します。
>
> Windows 10、バージョン 1803、以降、MBAE アプリ エクスペリエンスは、uWP アプリの概要については月に置換されます。 UWP アプリの月の概要については、次を参照してください。 [uWP モバイル ブロード バンド アプリの概要](uwp-mobile-broadband-apps.md)します。

Windows 8、Windows 8.1、および Windows 10 モバイル ブロード バンド アプリケーション エクスペリエンスのさまざまな側面をカスタマイズするメタデータを行うことができます。 PC をプロビジョニングする演算子をブランド化、Windows 接続マネージャーで、モバイル ブロード バンドのアプリの統合、Windows APN データベースの更新情報を提供すること、およびデータを提供する Windows 接続マネージャーのカスタマイズが含まれます。 Windows 8、Windows 8.1、および Windows 10 は、次の 3 つのソース メタデータを使用することができますにはが含まれています。

-   **Windows APN データベース**The Windows APN データベースには、最初に、オペレーターのネットワークに接続するために必要な事前プロビジョニング済みのデータが含まれています。 データベースでは、Windows 8、Windows 8.1、および Windows 10 の一部であるし、更新プログラムの概要については Windows を使用して更新されます。 Windows APN データベースは常に、PC でご確認いただけます。 COSA と APN データベースの詳細については、次を参照してください。 [COSA/APN データベース](cosa-apn-database.md)します。

-   **サービス メタデータ**サブスクリプションの購入と演算子のブランド化に必要な情報。 サービス メタデータ パッケージの一部としてこの情報を入力します。 Windows メタデータとインターネット サービス (WMIS) に格納されている、任意のインターネット接続を使用して、モバイル ブロード バンド デバイスが検出された後にダウンロードします。 OEM が PC 上にこのメタデータがプレインストールもできますが、Windows デベロッパー センター - ハードウェアのハードウェア開発」セクションからダウンロードされたパッケージをプレインストールする必要があります。 サービス メタデータの詳細については、次を参照してください。[サービス メタデータ](service-metadata.md)します。

-   **アカウント プロビジョニングのメタデータ**Wi-fi の資格情報およびプランの情報を含む、サブスクリプションの購入後に生成される情報。 このメタデータは Windows に支払いの検証後に自分で提供され、プロビジョニング更新メカニズムを使用して更新することができます。 アカウント プロビジョニングのメタデータに関する詳細については、次を参照してください。[アカウント プロビジョニング](account-provisioning.md)します。

次の図は、異なるメタデータ ソースはどのように関連し、処理する方法を示します。 サービス メタデータ Windows APN データベース内の情報よりも優先されます。

![これはモバイル ブロード バンドの概要](images/mbae-sxs-overview.jpg)

概要では、このセクションでは、リンクを使用して、モバイル ブロード バンド メタデータのさまざまな種類の詳細について説明します。

-   [アカウントの準備](account-provisioning.md)

-   [COSA/APN データベース](cosa-apn-database.md)

-   [サービス メタデータ](service-metadata.md)
