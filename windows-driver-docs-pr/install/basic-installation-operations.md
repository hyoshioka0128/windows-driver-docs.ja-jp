---
title: 基本のインストール操作
description: 基本のインストール操作
ms.assetid: 9bf1a3e1-6c2a-4f8c-8694-6e859a73d9a6
keywords:
- SetupAPI 関数 WDK、基本的なインストールの操作
- デバイスのインストールは、WDK SetupAPI を関数します。
- 一般的なセットアップは、WDK SetupAPI を関数します。
- SP_DEVINFO_DATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0671756fe6a075873f1296ddc07ce08d037bf99f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385637"
---
# <a name="basic-installation-operations"></a>基本のインストール操作





インストーラーが使用できる、[一般的なセットアップ関数](https://docs.microsoft.com/previous-versions/ff544985(v=vs.85))と[デバイス インストールの機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))SetupAPI インストール操作を実行する用意されています。 これらの関数は、を介して選択ダイアログ ボックスで、ユーザーに、ドライバーの選択肢を表示して、実際のドライバーのインストールを実行する、互換性のあるドライバーの INF ファイルを検索するインストーラーを許可します。

デバイスのインストール機能のほとんどの情報に依存、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)インストール タスクを実行する構造体。 各デバイスは、SP_DEVINFO_DATA 構造体に関連付けられます。 (HDEVINFO) のハンドルを取得することができます、[デバイス情報設定されている](device-information-sets.md)を使用して、特定のクラスにインストールされているすべてのデバイスを含む、 [ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)関数。 使用することができます、 [ **SetupDiCreateDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)デバイス情報のセットに新しいデバイスを追加する関数。 設定を使用してデバイス情報ですべての SP_DEVINFO_DATA 構造体を解放することができます、 [ **SetupDiDestroyDeviceInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist)関数。 この関数は、互換性のあるデバイスとクラス デバイス リストはすべて、構造に追加された可能性がありますも解放します。

使用して、 [ **SetupDiBuildDriverInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)関数の場合、インストーラーまたはユーザー選択可能なドライバーまたはをインストールするデバイス一覧を生成することができます。 **SetupDiBuildDriverInfoList**互換ドライバーの一覧または特定のクラスのすべてのデバイスの一覧を作成します。

互換性のあるドライバーの一覧を作成したらを使用して、一覧から選択するユーザーにダイアログを表示できます、 [ **SetupDiSelectDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)関数。 この関数では、デバイスの情報セット内の各デバイスに関する情報を含むダイアログ ボックスが表示されます。 使用して、選択したドライバーをインストールすることができます、 [ **SetupDiInstallDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)関数。 この関数は、必要に応じて、デバイスのハードウェアの構成を設定して、適切なディレクトリにドライバー ファイルをコピーするすべての新しいレジストリ エントリを作成するドライバーの INF ファイルの情報を使用します。

インストーラーは、確認し、デバイスのインストールの場合、レジストリ キーの値を設定する必要があります。 使用して、デバイスのハードウェアまたはドライバーのキーを開くことができます、 [ **SetupDiCreateDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)または[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)関数.

新しいをインストールする[デバイス セットアップ クラス](device-setup-classes.md)を使用して、 [ **SetupDiInstallClass** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassa)関数。 この関数は、含んでいる INF ファイルから新しいセットアップ クラスをインストール、 [ **INF ClassInstall32 セクション**](inf-classinstall32-section.md)します。

使用して、システムから、デバイスを削除することができます、 [ **SetupDiRemoveDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)関数。 この関数では、デバイスのレジストリ エントリを削除し、可能であれば、デバイスを停止します。 デバイスを動的に停止できない場合、関数は、最終的にユーザーがシステムをシャット ダウンするように求められますが発生するフラグを設定します。

 

 





