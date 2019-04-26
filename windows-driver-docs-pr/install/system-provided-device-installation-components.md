---
title: システム指定のデバイスのインストール コンポーネント
description: システム指定のデバイスのインストール コンポーネント
ms.assetid: faf586b9-ab99-4fee-a0d1-923000000189
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab257f2c828a30e599c7b951148b986c1e05fe75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339650"
---
# <a name="system-provided-device-installation-components"></a>システム指定のデバイスのインストール コンポーネント


次の一覧には、Windows オペレーティング システムによって提供されるデバイスのインストール コンポーネントについて説明します。

<a href="" id="plug-and-play--pnp--manager"></a>プラグ アンド プレイ (PnP) マネージャー  
プラグ アンド プレイ (PnP) マネージャーでは、Windows 内での PnP の機能を次のサポートを示します。

-   デバイスの検出と、システムの起動中に列挙型
-   追加またはシステムの実行中にデバイスを削除します。

詳細については、次を参照してください。 [PnP マネージャー](pnp-manager.md)します。

<a href="" id="setupapi"></a>SetupAPI  
セットアップ アプリケーション プログラミング インターフェイス (*SetupAPI*) 一般的なセットアップ関数が含まれています (**セットアップ * **Xxx*) とデバイスのインストール機能 (** SetupDi * **Xxx*と **Di * * * Xxx*)。 これらの関数は、INF ファイルの検索、潜在的なデバイスのドライバーの一覧を作成、ドライバー ファイルをコピー、レジストリに情報を書き込むおよび co-installer をデバイスの登録などの多くのデバイスのインストール タスクを実行します。 ほとんどの他のデバイスのインストール コンポーネントは、これらの関数を呼び出します。

詳細については、次を参照してください。 [SetupAPI](setupapi.md)します。

<a href="" id="configuration-manager-api"></a>Configuration Manager の API  
基本的なインストールと構成の操作には、SetupAPI によって提供されない PnP configuration manager の API を提供します。 PnP 構成マネージャーの機能は、デバイス ノードの状態の取得などの低レベルのタスクを実行 (*devnode*) とリソースの記述子を管理します。 これらの関数は、SetupAPI によって主に呼び出されますが、その他のデバイス インストールのコンポーネントによって呼び出すこともできます。

<a href="" id="driver-store"></a>ドライバー ストア  
Windows Vista 以降、ドライバー ストアは、インボックスとサード パーティの信頼できるコレクション[ドライバー パッケージ](driver-packages.md)します。 オペレーティング システムでは、ローカルのハード ディスク上のセキュリティで保護された場所で、このコレクションを保持します。 デバイスのドライバー ストアにドライバー パッケージのみをインストールできます。

詳細については、次を参照してください。[ドライバー ストア](driver-store.md)します。

<a href="" id="device-manager"></a>デバイス マネージャー  
デバイス マネージャーでは、表示し、システム上のデバイスを管理します。 たとえば、デバイスの状態を表示でき、デバイスのプロパティを設定できます。

詳細については、次を参照してください。[デバイス マネージャーを使用して](using-device-manager.md)します。 また、デバイス マネージャーのヘルプ ドキュメントを参照してください。

 

 





