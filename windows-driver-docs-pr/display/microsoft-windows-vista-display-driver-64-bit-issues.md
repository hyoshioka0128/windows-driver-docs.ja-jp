---
title: Windows Display Driver Model (WDDM) の 64 ビット問題
description: Windows Display Driver Model (WDDM) の 64 ビット問題
ms.assetid: ab391fca-bc98-4e98-9531-7a1d24ee173d
keywords:
- 64 ビットの WDK の表示
- ディスプレイ ドライバー モデル WDK Windows Vista では、64 ビット
- Windows Vista display driver モデル WDK、64 ビット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84d7b39693502caf703b0991ad69bf777b5788f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385603"
---
# <a name="windows-display-driver-model-wddm-64-bit-issues"></a>Windows Display Driver Model (WDDM) の 64 ビット問題


32 ビット アプリケーションを 64 ビットのオペレーティング システムで実行できるように、64 ビット アプリケーションを必要とする 64 ビット ユーザー モードのディスプレイ ドライバーだけでなく 32 ビット ユーザー モードのディスプレイ ドライバーを指定する必要があります。 ただし、64 ビットのオペレーティング システムでディスプレイのミニポート ドライバーの 64 ビット バージョンのみが必要です。 Windows (WOW64) 上の Windows では、64 ビットのオペレーティング システムで実行する 32 ビット アプリケーションを使用できます。 詳細については、次を参照してください。 [、64 ビット ドライバーをサポートしている 32 ビットの I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)します。

を 64 ビットのオペレーティング システムで 32 ビット ユーザー モードのディスプレイ ドライバーをインストールするには、グラフィックス デバイスのディスプレイのミニポート ドライバーの INF ファイルの追加レジストリ セクションで、次のエントリを設定する必要があります。 これは、ドライバーのインストール中にレジストリに 32 ビット ユーザー モードのディスプレイ ドライバーの DLL の名前を追加するために発生する必要があります。

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverNameWow, %REG_MULTI_SZ%, Xxx.dll
...
```

INF ファイルは、オペレーティング システム、システムの %systemroot% に 32 ビット ユーザー モードのディスプレイ ドライバーのコピーを特定する情報を含める必要があります\\SysWOW64 ディレクトリ。 詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)と[ **INF DestinationDirs セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)します。

WOW64 はなどの非透過または型指定されていないデータ構造を処理できないので、 [ **D3DDDICB\_ALLOCATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)経由で渡された構造体、 [ **pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数の場合、32 ビットから 64 ビットへの自動変換を実行できません。 そのため、正常に動作する WOW64 の 32 ビットのユーザー モードを記述する場合は、次の項目は、64 ビットのオペレーティング システムで実行するドライバーを表示を考慮する必要があります。

-   ポインターまたはデータの種類の複数のオペレーティング システムを機密として、サイズを避けるため\_T またはハンドル。 構造全体の変数のサイズを行うと共にこれらの可変幅のデータ型の配置と個々 のメンバーの位置は異なるを作成します。 可変幅のメンバーは避けられませんをデータ構造は、32 ビット ユーザー モードのディスプレイ ドライバーによって元を示すために別のメンバーを追加することができます。 正しく、64 ビット ディスプレイ ミニポート ドライバーでは、変換を実行できるからです。

-   可変幅のメンバーが存在しない場合でも、アーキテクチャ固有の配置要件を考慮する必要があります。 たとえば、x64 で UINT64 (または QWORD) は 8 バイトでアラインされます。 標準の 32 ビット コンパイラでコンパイルされた 32 ビット ユーザー モードのディスプレイ ドライバーはこれらのネイティブの 64 ビット型を正しく配置されない可能性があります、ため、64 ビット ディスプレイ ミニポート ドライバーが正確に 32 ビット ユーザー モードのディスプレイ ドライバーのデータにアクセスできません。 ただし、適切なを使用して配置を強制できます**プラグマ**コンパイラ ディレクティブ。 使用しても**プラグマ**コンパイラ ディレクティブは、32 ビットのオペレーティング システムではわずかな領域の無駄遣いを発生する可能性があります、32 ビットと 64 ビットのオペレーティング システムで同一の 32 ビット ユーザー モードのディスプレイ ドライバーを使用できます。 場合は、適切なを使用して配置を強制することはできません**プラグマ**コンパイラ ディレクティブでは、WOW64 を使用して、64 ビット オペレーティング システムで実行される 32 ビット ユーザー モードのディスプレイ ドライバーが 32 ビット ユーザー モードのディスプレイ ドライバーとは異なる必要があります32 ビットのオペレーティング システムで実行されています。

 

 





