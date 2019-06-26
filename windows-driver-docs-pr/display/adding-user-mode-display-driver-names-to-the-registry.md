---
title: レジストリへのユーザー モード ディスプレイ ドライバー名の追加
description: レジストリへのユーザー モード ディスプレイ ドライバー名の追加
ms.assetid: 52f98ce5-4458-4058-9134-f57e4b56377f
keywords:
- INF ファイル WDK の表示、ユーザー モード ドライバー名
- ユーザー モード ドライバー WDK Windows Vista では、レジストリに追加の名前を表示します。
- レジストリ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b957581c6c4adc7de84a7cb9228412e47493fa1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353451"
---
# <a name="adding-user-mode-display-driver-names-to-the-registry"></a>レジストリへのユーザー モード ディスプレイ ドライバー名の追加


ユーザー モードのディスプレイ ドライバーの名前がドライバーのインストール中にレジストリに追加されるよう、INF ファイルの追加レジストリ セクションで、次のエントリを設定する必要があります。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, UserModeDriverName1, UserModeDriverName2, UserModeDriverNameWow1, UserModeDriverNameWow2
```

たとえば、x86 コンピューター。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, r200umd 
```

たとえば、x64 コンピューター。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, r200umd, r200umdva, r200umd64, r200umd64va
```

Microsoft Windows Hardware Quality Labs (WHQL) テスト プログラムでは、ユーザー モード ドライバーの表示名のリストを使用して、検証テストの実行をドライバー バイナリが変わりません。 他のアプリケーションが経由で使用もユーザー モード ドライバーの表示名の一覧通常[を実装する WMI](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) の一部である、アプリケーションを決定するファイルのリストとして、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package).

 

 





