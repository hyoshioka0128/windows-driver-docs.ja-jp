---
title: ユーザー モード ディスプレイ ドライバーの読み込み
description: ユーザー モード ディスプレイ ドライバーの読み込み
ms.assetid: bfebe590-bcde-40cf-9074-8d0f63e0562d
keywords:
- INF ファイル WDK の表示、ユーザー モード ドライバーの読み込み
- ディスプレイ ドライバーの読み込み、WDK の Windows Vista のユーザー モード
- WDK を表示するドライバーの読み込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a923ee29e3a66ad071ccfb96e5ff1e143d05fcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380383"
---
# <a name="loading-a-user-mode-display-driver"></a>ユーザー モード ディスプレイ ドライバーの読み込み


ドライバーのインストール中にユーザー モードのディスプレイ ドライバーの DLL の名前をレジストリに追加して、マイクロソフトの Direct3D ランタイムでは、DLL を読み込むことができます、その後ように INF ファイルの追加レジストリ セクションで、次のエントリを設定する必要があります。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDriverName,    %REG_MULTI_SZ%, Xxx.dll
```

INF ファイルは、オペレーティング システム、システムの %systemroot% に、ユーザー モードのディスプレイ ドライバーのコピーを特定する情報を含める必要があります\\system32 ディレクトリ。 詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)と[ **INF DestinationDirs セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)します。

Direct3D のランタイムは、ランタイムのプロセス空間内でユーザー モードのディスプレイ ドライバーを読み込むために、レジストリからユーザー モードのディスプレイ ドライバーの DLL の名前を取得します。

 

 





