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
ms.openlocfilehash: 823b56df8251bfcd2c3bc2843b6ecc0e8ccbc52b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341591"
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

Microsoft Windows Hardware Quality Labs (WHQL) テスト プログラムでは、ユーザー モード ドライバーの表示名のリストを使用して、検証テストの実行をドライバー バイナリが変わりません。 他のアプリケーションが経由で使用もユーザー モード ドライバーの表示名の一覧通常[を実装する WMI](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI) の一部である、アプリケーションを決定するファイルのリストとして、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff539954).

 

 





