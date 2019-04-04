---
title: PSHED プラグインを開発するためのロードマップ
description: PSHED プラグインを開発するためのロードマップ
ms.assetid: 3e1eb744-e480-4478-9705-94da8029c382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b59a3972ad9a9e09a08da880ace307e68d096f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560169"
---
# <a name="roadmap-for-developing-pshed-plug-ins"></a>PSHED プラグインを開発するためのロードマップ


![コンパス、マップ、および指でマップ ポイントの図](images/map-hand-sml.png)

プラットフォーム固有のハードウェア エラー ドライバー (PSHED) は、プラットフォーム固有のエラー情報を収集するために使用される Windows ハードウェア エラー アーキテクチャ (WHEA) のコンポーネントです。 PSHED このレイヤーを提供することで、基になるプラットフォームのハードウェア エラー報告機能の上に抽象化レイヤーを提供する、PSHED 処理機能、オペレーティング システムからプラットフォームのエラーの詳細を非表示にし、公開します。一貫性のあるエラーが Windows オペレーティング システムへのインターフェイスを処理します。

ハードウェア エラーのリソースを処理するシステム ファームウェア インターフェイスに関連するプラットフォームでは、PSHED は、ファームウェアのインターフェイスを管理します。 この機能を使用するには、プラットフォーム ベンダーによって実装される PSHED プラグインを使用します。

PSHED のプラグインは、Windows driver model (WDM) に基づいており、ハードウェア プラットフォームのレポートと回復の機能のエラーをソフトウェア インターフェイスを提供するドライバーです。

プラグイン PSHED は、プラットフォーム ベンダーによって定義されているプライベート インターフェイスを使用しても、プラットフォーム ファームウェアと対話できます。 これにより、既存のファームウェアを使用して、ハードウェア エラーの処理を続行する、プラットフォーム ベンダーができます。

Windows Vista および Windows の以降のバージョン用の PSHED プラグイン ドライバーを作成するには、次の手順を実行します。

-   手順 1:Windows アーキテクチャとドライバーについて説明します。

    まず、Windows オペレーティング システムでのドライバーのしくみの基礎を理解する必要があります。 基礎を知ることに役立つ適切な設計上の決定を行い、開発プロセスを効率化することができます。

    ドライバーの基礎の詳細については、[理解ドライバーとオペレーティング システムの基礎](https://msdn.microsoft.com/library/windows/hardware/ff554731)を参照してください。

-   手順 2:Windows ハードウェア エラー アーキテクチャ (WHEA) の基礎について説明します。

    、Windows Vista で導入された、WHEA では、以前のバージョンの Windows では、ハードウェアのエラー レポート機能を拡張し、一貫性のあるハードウェア エラー インフラストラクチャのコンポーネントとして、これらのメカニズムをまとめます。 WHEA は今日のハードウェア デバイスで使用でき、システム ファームウェアとより密接に統合する追加のハードウェア エラー情報を使用します。

    Windows Vista で WHEA の基礎と以降のバージョンの Windows を理解する必要があります。 これからは、WHEA で、適切な設計上の決定をするのに役立つもの機能コンポーネントを理解できます。

    WHEA の詳細については、[、Windows Hardware Error Architecture の概要](introduction-to-the-windows-hardware-error-architecture.md)と[Windows ハードウェア エラー アーキテクチャの概要](windows-hardware-error-architecture-overview.md)を参照してください。

-   手順 3:Windows ドライバーのビルド、テスト、およびデバッグ プロセスおよびツールについて説明します。

    ドライバーの構築は、ユーザー モード アプリケーションを構築することと同じではありません。

    Windows ドライバーのビルド、デバッグ、およびテスト プロセス、ドライバーの署名、および Windows のロゴ テストについては、[のビルド、デバッグ、およびテスト ドライバー](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)を参照してください。

    ビルドの詳細については、テスト、検証、およびデバッグ ツールを参照してください[ドライバー開発ツール](https://msdn.microsoft.com/library/windows/hardware/ff545440)します。

-   手順 4:プラグイン、PSHED に関する設計上の決定を行います。

    プラグイン、PSHED のデザインを開始する前に、次の最初に理解する必要があります。

    -   機能要件と、Windows Vista 用の PSHED プラグインの操作および以降のバージョンの Windows。

        詳細については、[プラットフォームに固有のハードウェア エラー ドライバー プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)を参照してください。

    -   Windows Vista 以降に行われた WHEA に変更します。

        これらの変更の詳細については、[Windows Hardware Error Architecture の新しい情報](new-information-for-windows-hardware-error-architecture.md)を参照してください。

-   手順 5:開発、構築、テストし、PSHED プラグインをデバッグします。

    次のトピックの情報を使用すると、プラグイン PSHED の動作を正しくビルドできます。

    -   PSHED のプラグインの開発に関するガイドラインについては、[PSHED プラグイン ガイドライン](pshed-plug-in-guidelines.md)を参照してください。
    -   プラグインの PSHED を構築する方法については、[構築プラグイン PSHED](building-a-pshed-plug-in.md)を参照してください。
    -   プラグインの PSHED をデバッグするために使用する WHEA デバッガー拡張機能については、[Windows ハードウェア エラー アーキテクチャ デバッガー拡張](windows-hardware-error-architecture-debugger-extensions.md)を参照してください。
    -   反復的なビルド、テスト、およびデバッグについては、[概要のビルド、デバッグ、およびテスト プロセス](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)を参照してください。
-   手順 6:プラグイン、PSHED のドライバー パッケージを作成します。

    PSHED のプラグインは、WDM ドライバーです。 使用して他の WDM ドライバー PSHED プラグインがインストールされている、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)します。

    ドライバー パッケージの詳細については、[ドライバー パッケージを提供する](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)を参照してください。

    プラグインの PSHED をドライバー パッケージをインストールする方法の詳細については、[PSHED プラグイン インストール](pshed-plug-in-installation.md)を参照してください。

-   手順 7:署名し、プラグイン、PSHED を配布します。

    最後の手順では、デジタル署名と配布、PSHED をプラグインします。 PSHED プラグインは、すべての既存の Windows Hardware Quality Labs (WHQL) テスト プログラムには適合しません。 そのため、PSHED プラグインは、Authenticode 署名を使用してデジタル署名する必要があります。

    署名と配布、PSHED プラグインの詳細については、[見極めと配布 PSHED プラグイン](qualifying-and-distributing-pshed-plug-ins.md)を参照してください。

これらは、基本的な手順です。 追加の手順は、個々 の PSHED プラグインのニーズに合わせては入力が必要な可能性がありますに。

 

 




