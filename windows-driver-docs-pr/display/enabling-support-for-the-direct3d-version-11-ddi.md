---
title: Direct3D のバージョン 11 DDI のサポートを有効にします。
description: Direct3D のバージョン 11 DDI のサポートを有効にします。
ms.assetid: 997d6b06-110b-403d-bcf5-350a26ecffbd
keywords:
- DDI サポートを有効にすると、Direct3D バージョン 11 WDK Windows 7 表示
- DDI サポートを有効にすると、Direct3D バージョン 11 WDK Windows Server 2008 R2 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73bdda91b8dee52a87bddf59585efbc610e9e1c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536533"
---
# <a name="enabling-support-for-the-direct3d-version-11-ddi"></a>Direct3D のバージョン 11 DDI のサポートを有効にします。


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

11 DDI、INF ファイルをユーザー モード ディスプレイ ドライバー DLL のバージョンがグラフィックス デバイスかどうかに関係なく、DLL の名前をリストする必要があります、ディスプレイ ドライバーをインストール用にサポートを有効にする Direct3D のバージョン 11 DDI が存在するのと同じ DLL、 [Direct3D のバージョン 9 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552927)と[Direct3D のバージョン 10 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552909)または個別の DLL にします。

[ミニポートの表示と表示のユーザー モード ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)セクションは、ユーザー モードのディスプレイ ドライバーがインストールされ、Windows Vista のディスプレイ ドライバー モデルに従って使用する方法について説明します。 有効にするためのサポート、Direct3D のバージョン 11 DDI、バージョン 11 が含まれている DLL の名前を指定する必要がありますのバージョン 11 DDI が存在する場合でも、ユーザー モードの一覧で、3 番目のエントリとして DDI はドライバー名を表示、バージョン 9 と 10 Ddi として同じ DLL。

複数の場所に同じユーザー モードのディスプレイ ドライバー DLL 名を使用すると、統合するドライバーを実装します。 実際には、Direct3D のバージョン 10 とバージョン 11 Ddi の設計では、厳密に Direct3D のバージョン 10 と Direct3D のバージョン 11 ドライバーの共有の実装をサポートします。

次のバージョン 11 DDI に含まれる場合に、例に示すどのバージョンのサポートは 11 DDI が有効になっている*Umd11*.dll (バージョン 9 と 10 Ddi から独立した DLL)。

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd9.dll, umd10.dll,  umd11.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd9, umd10, umd11 
```

次のバージョン 11 DDI に含まれる場合に、例に示すどのバージョンのサポートは 11 DDI が有効になっている*Umd*.dll (Direct3D のバージョン 9、10 および 11 のドライバーの共有実装)。

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd.dll, umd.dll, umd.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd, umd, umd 
```

 

 





