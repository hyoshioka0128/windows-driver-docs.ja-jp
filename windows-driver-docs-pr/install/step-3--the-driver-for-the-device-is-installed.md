---
title: 手順 3. デバイスのドライバーがインストールされている
description: 手順 3. デバイスのドライバーがインストールされている
ms.assetid: 292c5ffe-fbdf-42b8-9642-024c78709843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68769629b495c659fa6bd35383c83e58c276b62c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837357"
---
# <a name="step-3-the-driver-for-the-device-is-installed"></a>手順 3: デバイスのドライバーがインストールされている


Windows が新しいデバイスに最適なドライバーを選択すると、デバイスとドライバーに関する情報が次のように保存されます。

-   同じモデルとバージョンの複数のデバイスをコンピューターに接続できます。 各デバイス接続は、*デバイスインスタンス*と呼ばれます。

    Windows は、各デバイスインスタンスを一意のデバイスノード (*devnode*) として表します。 Devnode には、デバイスが起動したかどうかや、デバイスで通知するために登録されているドライバーなど、デバイスに関する情報が含まれています。

-   Windows は、デバイスのドライバーを*ドライバーノード*として表します。 ドライバーノードは、[ドライバーパッケージの](driver-packages.md) [Inf ファイル](overview-of-inf-files.md)の[**inf*モデル*セクション**](inf-models-section.md)内の一致するデバイスエントリの情報に基づいています。 ドライバーノードには、すべてのサービス、デバイス固有の共同インストーラー、レジストリエントリなど、デバイスのすべてのソフトウェアサポートが含まれています。

デバイスとドライバーがインスタンス化されるとすぐに、Windows は次の手順に従ってドライバーをインストールします。

1.  [ドライバーパッケージの](driver-packages.md) [INF ファイル](overview-of-inf-files.md)内のディレクティブに基づいて、Windows は次のことを行います。

    -   [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)で指定されているように、ドライバーバイナリとその他の関連ファイルをハードディスク上の場所にコピーします。

    -   レジストリキーの書き込みなど、デバイスインスタンス関連の構成を実行します。

2.  Windows は、[ドライバーパッケージの](driver-packages.md) [inf ファイル](overview-of-inf-files.md)の [ [**Inf バージョン] セクション**](inf-version-section.md)の**クラス**および**classguid**エントリから[デバイスセットアップクラス](device-setup-classes.md)を決定します。 デバイスのインストールを最適化するために、同じ方法でセットアップおよび構成されたデバイスは、同じデバイスのセットアップクラスにグループ化されます。

3.  ドライバーファイルがコピーされるとすぐに、Windows は[プラグアンドプレイ (PnP) マネージャー](pnp-manager.md)に制御を転送します。 PnP マネージャーはドライバーを読み込み、デバイスを起動します。

4.  PnP マネージャーは、適切な関数ドライバーと、デバイスの任意のオプションのフィルタードライバーを読み込みます。

    PnP マネージャーは、まだ読み込まれていない必要なドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出します。 次に、PnP マネージャーは、ドライバーごとに[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出します。これは、フィルタードライバーが低いドライバーから開始され、関数ドライバーと、最後にフィルタードライバーが適用されます。 PnP マネージャーは、必要に応じて、デバイスにリソースを割り当て、デバイスのドライバーに[**IRP_MN_START_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を送信します。

この手順が完了するとすぐに、デバイスがインストールされ、使用できる状態になります。

 

 





