---
title: ユーザー モードのディスプレイ ドライバーの読み込み
description: ユーザー モードのディスプレイ ドライバーの読み込み
ms.assetid: bfebe590-bcde-40cf-9074-8d0f63e0562d
keywords:
- INF ファイル WDK の表示、ユーザー モード ドライバーの読み込み
- ディスプレイ ドライバーの読み込み、WDK の Windows Vista のユーザー モード
- WDK を表示するドライバーの読み込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81932134fbd1d5f3500ac576a3bc0703dd19f72a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549230"
---
# <a name="loading-a-user-mode-display-driver"></a>ユーザー モードのディスプレイ ドライバーの読み込み


ドライバーのインストール中にユーザー モードのディスプレイ ドライバーの DLL の名前をレジストリに追加して、マイクロソフトの Direct3D ランタイムでは、DLL を読み込むことができます、その後ように INF ファイルの追加レジストリ セクションで、次のエントリを設定する必要があります。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDriverName,    %REG_MULTI_SZ%, Xxx.dll
```

INF ファイルは、オペレーティング システム、システムの %systemroot% に、ユーザー モードのディスプレイ ドライバーのコピーを特定する情報を含める必要があります\\system32 ディレクトリ。 詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)と[ **INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383)します。

Direct3D のランタイムは、ランタイムのプロセス空間内でユーザー モードのディスプレイ ドライバーを読み込むために、レジストリからユーザー モードのディスプレイ ドライバーの DLL の名前を取得します。

 

 





