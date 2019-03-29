---
title: Boot.ini ファイルの概要
description: Boot.ini ファイルは、BIOS ファームウェアを Windows Vista より前の NT ベースのオペレーティング システムを実行しているコンピューターのブート オプションを含むテキスト ファイルです。 システム パーティション、c:\Boot.ini 通常のルートになります。
ms.assetid: bc9bb063-4caa-42fe-bb3d-dc588fbbb8d9
keywords:
- Boot.ini ファイル WDK、Boot.ini ファイルについて
- ブート ローダー セクション WDK ブート オプション
- オペレーティング システム セクションの WDK ブート オプション
- WDK のブート エントリ
- WDK のブート オプションの名前
- WDK のブート オプションのフレンドリ名
- ブート エントリ パラメーター WDK
- WDK のブート パラメーター
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d0193b302f5a4101775cbfef2050c3b12e48e5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573771"
---
# <a name="overview-of-the-bootini-file"></a>Boot.ini ファイルの概要

> [!IMPORTANT] 
> このトピックでは、Windows XP および Windows Server 2003 でサポートされるブート オプションについて説明します。 Windows の最新バージョンのブート オプションを変更する場合は、次を参照してください。 [Windows Vista 以降のブート オプション](boot-options-in-windows-vista-and-later.md)します。

Boot.ini ファイルは、BIOS ファームウェアを Windows Vista より前の NT ベースのオペレーティング システムを実行しているコンピューターのブート オプションを含むテキスト ファイルです。 通常は c: のシステム パーティションのルートにある\\Boot.ini します。 次の例では、一般的な Boot.ini ファイルの内容を示します。

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
C:\CMDCONS\BOOTSECT.DAT="Microsoft Windows Recovery Console" /cmdcons
```

Boot.ini では、2 つの主要なセクションがあります。

-   **\[ブート ローダー\]** セクションには、システムのブート エントリをすべてに適用されるオプションの設定が含まれています。 オプションとして、**タイムアウト**、ブート メニュー タイムアウト値、および**既定**既定のオペレーティング システムの場所。

    次のサンプルに示します、\[ブート ローダー\] Boot.ini のセクション。

    ```
    [boot loader]
    timeout=30
    default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   **\[オペレーティング システム\]** セクションが 1 つまたは複数で構成される*ブート エントリ*の各オペレーティング システムまたは起動可能なプログラムがコンピューターにインストールされています。

    A*ブート エントリの*は、オペレーティング システムまたは起動可能なプログラムのロード構成を定義するオプションのセットです。 ブート エントリは、オペレーティング システムまたは起動可能なプログラムとそのファイルの場所を指定します。 オペレーティング システムまたはプログラムを構成するパラメーター型を含めることもできます。

    次のサンプルに示します、\[オペレーティング システム\]Boot.ini の 2 つのオペレーティング システム、Microsoft Windows XP と Microsoft Windows 2000 コンピューターでのセクション。 オペレーティング システムごとに 1 つ、2 つのブート エントリがあります。

    ```
    [operating systems]
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
    multi(0)disk(0)rdisk(0)partition(2)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
    ```

各ブート エントリには、次の要素が含まれています。

-   オペレーティング システムの場所。 Boot.ini は、オペレーティング システムが存在する場所のディスクのパーティション分割とディレクトリ パスを表示するのに Advanced RISC コンピューティング (弧) の名前付け規則を使用します。 以下に例を示します。
    ```
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   ブート エントリのフレンドリ名。 フレンドリ名は、ブート メニューのブート エントリを表します。 フレンドリ名では、引用符で囲まれているし、ブート メニューのブート エントリを表します。 例:
    ```
    "Microsoft Windows XP Professional"
    ```

-   *ブート エントリのパラメーター*とも呼ばれます*ブート パラメーター*または*ロード オプション*有効化、無効化、およびオペレーティング システムの機能を構成します。 ようなコマンド ライン パラメーター、フォワード スラッシュ (/) で始まるなどをブート パラメーター [ **/debug**](https://msdn.microsoft.com/library/windows/hardware/ff556253)します。 各ブート エントリには、0 個以上のブート パラメーターがあります。

    ドライバーのテストとデバッグに関連するブート パラメーターの一覧は、次を参照してください。 [Boot.ini のブート パラメーター参照](https://msdn.microsoft.com/library/windows/hardware/ff542248)します。

それぞれ異なる一連のブート パラメーターを持つ、同じオペレーティング システムの複数のブート エントリがあることができます。 Windows 標準のブートを作成するエントリ、オペレーティング システムをインストールして、その他を作成するときに、Boot.ini を編集してオペレーティング システムのエントリをカスタマイズします。
