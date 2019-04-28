---
title: Direct3D バージョン 10 DDI のサポートの有効化
description: Direct3D バージョン 10 DDI のサポートの有効化
ms.assetid: ccbfecd2-8609-4e59-ac43-911f57af7980
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 24e2d6a58a784ea894eec8bfb506c36b74c90966
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379485"
---
# <a name="enabling-support-for-the-direct3d-version-10-ddi"></a>Direct3D バージョン 10 DDI のサポートの有効化


DDI 10、INF ファイルをユーザー モード ディスプレイ ドライバー DLL のバージョンがグラフィックス デバイスかどうかに関係なく、DLL の名前をリストする必要があります、ディスプレイ ドライバーをインストール用にサポートを有効にする Direct3D のバージョン 10 DDI が存在するのと同じ DLL、 [Direct3D のバージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/display/direct3d-functions-implemented-by-user-mode#direct3d-version-9-functions)または個別の DLL にします。

[ミニポートの表示と表示のユーザー モード ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)セクションは、ユーザー モードのディスプレイ ドライバーがインストールされ、Windows Vista のディスプレイ ドライバー モデルに従って使用する方法について説明します。 有効にするバージョンのサポートは、Direct3D DDI 10、10 のバージョンを含んでいる DLL の名前を指定する必要がありますユーザー モード ディスプレイ ドライバー名場合でもの一覧で、2 番目のエントリとして DDI 9 DDI バージョンと同じ DLL に存在する DDI 10 のバージョン。 次バージョン 10 で DDI が含まれている場合に、例を表示する方法、バージョンのサポートは DDI 10 が有効になっている*Umd10*.dll (バージョン 9 から別の DLL は、DDI)。

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd9.dll, umd10.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd9, umd10 
```

次バージョン 10 で DDI が含まれている場合に、例を表示する方法、バージョンのサポートは DDI 10 が有効になっている*Umd*.dll (バージョン 9 とは、同じ DLL DDI)。

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd.dll, umd.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd, umd 
```

 

 





