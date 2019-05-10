---
title: 手順 3 のデバイス ドライバーがインストールされています。
description: 手順 3 のデバイス ドライバーがインストールされています。
ms.assetid: 292c5ffe-fbdf-42b8-9642-024c78709843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08947e850224be9cf3e7cc53dad24eb5846a8f41
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65456420"
---
# <a name="step-3-the-driver-for-the-device-is-installed"></a>手順 3:デバイスのドライバーがインストールされます


Windows が新しいデバイスの最適なドライバーを選択すると後、は、次のように、デバイスとドライバーに関する情報を保存します。

-   同じモデルとバージョンの複数のデバイスは、コンピューターに接続できます。 各デバイスの接続と呼ばれる、*デバイス インスタンス*します。

    Windows は、一意のデバイス ノードとして各デバイスのインスタンスを表します (*devnode*)。 Devnode には、デバイスが開始されたかどうかや、どのドライバーがデバイスに通知に登録しているなど、デバイスに関する情報が含まれています。

-   Windows とデバイスのドライバーを表す、*ドライバー ノード*します。 ドライバー ノードが一致するデバイス エントリ内からの情報に基づいて、 [ **INF*モデル*セクション**](inf-models-section.md)の[ドライバー パッケージの](driver-packages.md) [INF ファイル](overview-of-inf-files.md)します。 ドライバー ノードには、任意のサービス、デバイスに固有の共同インストーラー、およびレジストリ エントリなど、デバイスのすべてのソフトウェアのサポートが含まれています。

デバイスとドライバーをインスタンス化するとすぐに Windows には、次の手順に従って、ドライバーがインストールされます。

1.  ディレクティブ内に基づく、[ドライバー パッケージの](driver-packages.md) [INF ファイル](overview-of-inf-files.md)Windows は次の処理します。

    -   ドライバーのバイナリ、およびその他の関連で指定したとおり、ハード_ディスク上の場所にファイルのコピー、 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)します。

    -   レジストリ キーの書き込みなど、どのデバイス インスタンスの関連する構成を実行します。

2.  Windows の決定、[デバイス セットアップ クラス](device-setup-classes.md)から、**クラス**と**ClassGuid**内のエントリ、 [ **INF バージョン セクション**](inf-version-section.md)の[ドライバー パッケージの](driver-packages.md) [INF ファイル](overview-of-inf-files.md)します。 デバイスのインストールを最適化するために設定され、同じ方法で構成されているデバイスは、同じデバイス セットアップ クラスに分類されます。

3.  Windows 転送ドライバー ファイルをコピーすると、すぐに制御を[プラグ アンド プレイ (PnP) manager](pnp-manager.md)します。 PnP マネージャーでは、ドライバーをロードし、デバイスを開始します。

4.  PnP マネージャーでは、関数の適切なドライバーとデバイスのすべてのオプションのフィルター ドライバーを読み込みます。

    PnP マネージャー呼び出し、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)がまだ読み込まれていない任意の必要なドライバーの日常的な。 PnP マネージャーを呼び出して、 [ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)以降、低いフィルター ドライバーでは、各ドライバー関数ドライバー、し、最後に、上部のフィルター ドライバーの日常的な。 PnP マネージャーは、必要な場合は、リソースをデバイスに割り当てられます。 し、送信、 [ **IRP_MN_START_DEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff551749)デバイスのドライバーにします。

このステップが完了するとすぐに、デバイスがインストールされ、すぐに使用できます。

 

 





