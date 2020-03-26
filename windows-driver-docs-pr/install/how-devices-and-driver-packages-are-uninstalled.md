---
title: デバイスとドライバー パッケージのアンインストール方法
description: デバイスとドライバー パッケージのアンインストール方法
ms.assetid: 0f4f0bbf-ca8f-47ef-b70b-d023bba9b842
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54bde8a616e73ea31ea4115f2f1899a3caebbb5
ms.sourcegitcommit: 7dff2005387294dbfeeec45c801bf6b4a4cb9319
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80261284"
---
# <a name="how-devices-and-driver-packages-are-uninstalled"></a>デバイスとドライバー パッケージのアンインストール方法


このセクションでは、デバイスと[ドライバーパッケージ](driver-packages.md)をアンインストールするために必要な作業の概要について説明します。 次のいずれかを実行して、これらの操作を実行します。

-   [デバイスマネージャー](using-device-manager.md)。

-   [Setupapi.log](setupapi.md)および[デバイスのインストール](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))機能を呼び出すデバイスインストールアプリケーション。

次の操作はその例です。

-   [デバイスをアンインストールしています](#uninstalling-the-device)

-   [ドライバーストアからドライバーパッケージを削除する](#deleting-a-driver-package-from-the-driver-store)

-   インストールされているドライバーのバイナリファイルを削除する

これらの操作を順番に実行する必要は  ない**ことに注意**してください。

 

### <a name="uninstalling-the-device"></a><a href="" id="uninstalling-the-device"></a>デバイスをアンインストールしています

このアンインストール操作により、システム内のデバイスの物理インスタンスを表すデバイスノード (*devnode*) が削除されます。 Devnodes は、次のいずれかの方法を使用して削除されます。

-   デバイス マネージャー。 詳細については、「[デバイス マネージャーの使用](using-device-manager.md)」を参照してください。

-   [**DIF_REMOVE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove)の要求を使用して、 [Setupapi.log](setupapi.md) [**setupdicallclassinstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)関数を呼び出すデバイスインストールアプリケーション。 詳細については、「[汎用セットアップ関数の使用](using-general-setup-functions.md)」を参照してください。

-   Setupapi.log 関数 (windows 7 以降のバージョンの Windows) を[**呼び出すデバイスインストール**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diuninstalldevice)アプリケーションです。 詳細については、「[デバイスインストール機能の使用](using-device-installation-functions.md)」を参照してください。

これらの方法のいずれかを使用してデバイスをアンインストールすると、プラグアンドプレイ (PnP) マネージャーは、デバイスのインストール中に作成されたシステム状態のサブセットを削除します。 たとえば、ドライバーのバイナリファイルとデバイスの関連付けが削除されます。 この関連付けは、サービスコントロールマネージャー (SCM) によって、デバイスの適切なドライバーを読み込むために使用されます。

このアンインストール操作では、インストール処理中に実行されたすべての操作が元に戻されるわけではありません。 たとえば、ドライバーパッケージまたは*共同インストーラー* (およびその他のいくつかのレジストリ操作) は変更されません。

**注**  このアンインストール操作の完了後は、デバイスの devnode が存在しなくなりますが、ドライバー[パッケージ](driver-packages.md)は[ドライバーストア](driver-store.md)にまだ存在しています。 PnP マネージャーがデバイスを再列挙した場合 (デバイスが取り外されてから再び接続された場合など)、PnP マネージャーはそれを新しいデバイスインスタンスとして扱い、ドライバーストアからドライバーパッケージをインストールします。

 

### <a name="deleting-a-driver-package-from-the-driver-store"></a><a href="" id="deleting-a-driver-package-from-the-driver-store"></a>ドライバーストアからドライバーパッケージを削除する

このアンインストール操作は、ドライバー[パッケージ](driver-packages.md)に関連付けられているファイルを[ドライバーストア](driver-store.md)から削除し、関連付けられているメタデータを PnP マネージャーの内部データベースから削除します。 この操作により、ドライバーパッケージに関連付けられている[inf ファイル](overview-of-inf-files.md)もシステムの inf ディレクトリから削除されます。

ドライバーパッケージをドライバーストアから削除した後は、デバイスにインストールできなくなります。 ドライバーパッケージは、光学メディア、ネットワーク共有、Windows Update など、元のソースの[ドライバーストア](driver-store.md)に再ステージングし、インストールする必要があります。

ドライバーパッケージをドライバーストアから削除する前に、そのパッケージを使用しているすべてのデバイスをアンインストールしてください。

**重要**  ドライバー[パッケージ](driver-packages.md)を[ドライバーストア](driver-store.md)から手動で削除することはできません。 これにより、INF xfs、ドライバーストアカタログ、およびドライバーストア内のドライバーの間で不整合が発生する可能性があります。 また、同じドライバーパッケージをドライバーストアにステージングできない場合もあります。

 


 

 





