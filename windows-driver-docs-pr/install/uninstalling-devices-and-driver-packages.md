---
title: デバイスとドライバー パッケージのアンインストール
description: デバイスとドライバー パッケージのアンインストール
ms.assetid: 4381ee42-778b-402d-b242-892ec921c28f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d35ac477ef83ca28c2a23b5b4adaeb90e54af305
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339459"
---
# <a name="uninstalling-devices-and-driver-packages"></a>デバイスとドライバー パッケージのアンインストール


デバイスがインストールされた後、デバイスをアンインストールする必要ありますまたは[ドライバー パッケージ](driver-packages.md)します。 たとえば、エンドユーザーが、関連付けられているデバイスに置き換えることや、ドライバー パッケージがドライバーが更新されたときにアンインストールする必要があります。

デバイスをアンインストールする場合は、デバイス ノードを削除する必要があります (*devnode*) システムで、デバイスの物理インスタンスを表します。

アンインストールすると、[ドライバー パッケージ](driver-packages.md)、次の操作を完了する必要があります。

-   関連付けられているファイルを削除、[ドライバー パッケージ](driver-packages.md)から、[ドライバー ストア](driver-store.md)します。

-   ドライバー パッケージのバイナリ ファイルを削除します。

このセクションでは、デバイスとドライバー パッケージをアンインストールする方法について説明します。 顧客に指示またはツールを提供するドライバー開発者向け。

ここでは、次のトピックについて説明します。

[デバイスとドライバー パッケージをアンインストールする方法](how-devices-and-driver-packages-are-uninstalled.md)

[デバイス マネージャーを使用して、デバイスとドライバー パッケージをアンインストールするには](using-device-manager-to-uninstall-devices-and-driver-packages.md)

[SetupAPI を使用して、デバイスとドライバー パッケージをアンインストールするには](using-setupapi-to-uninstall-devices-and-driver-packages.md)



