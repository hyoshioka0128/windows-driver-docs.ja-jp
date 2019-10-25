---
title: Boot.ini ファイルの概要
description: Boot.ini ファイルは、Windows Vista より前の NT ベースのオペレーティングシステムを実行している BIOS ファームウェアを搭載したコンピューターのブートオプションを含むテキストファイルです。 これは、システムパーティションのルート (通常は c:\Boot.ini.) にあります。
ms.assetid: bc9bb063-4caa-42fe-bb3d-dc588fbbb8d9
keywords:
- Boot.ini ファイルの WDK、boot.ini ファイルについて
- ブートローダーセクション WDK ブートオプション
- オペレーティングシステムセクション WDK ブートオプション
- ブートエントリ WDK
- 名前 WDK ブートオプション
- フレンドリ名 WDK ブートオプション
- ブートエントリパラメーター WDK
- ブートパラメーター WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: b31baf30ff2ca4be02fb273b1f7c46ad6d443a48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839336"
---
# <a name="overview-of-the-bootini-file"></a>Boot.ini ファイルの概要

> [!IMPORTANT] 
> このトピックでは、Windows XP と Windows Server 2003 でサポートされているブートオプションについて説明します。 Windows の最新バージョンのブートオプションを変更する場合は、「 [Windows Vista 以降のブートオプション](boot-options-in-windows-vista-and-later.md)」を参照してください。

Boot.ini ファイルは、Windows Vista より前の NT ベースのオペレーティングシステムを実行している BIOS ファームウェアを搭載したコンピューターのブートオプションを含むテキストファイルです。 これは、システムパーティションのルート (通常は c:\\Boot.ini) にあります。 次のサンプルは、一般的な boot.ini ファイルの内容を示しています。

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
C:\CMDCONS\BOOTSECT.DAT="Microsoft Windows Recovery Console" /cmdcons
```

Boot.ini には、次の2つの主要なセクションがあります。

-   **\[ブートローダーの\]** セクションには、システム上のすべてのブートエントリに適用されるオプション設定が含まれています。 オプションには、**タイムアウト**、ブートメニューのタイムアウト値 **、既定の**オペレーティングシステムの場所などがあります。

    次のサンプルは、boot.ini の \[ブートローダー\] セクションを示しています。

    ```
    [boot loader]
    timeout=30
    default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   **\[オペレーティングシステム\]** セクションは、コンピューターにインストールされているオペレーティングシステムまたは起動可能なプログラムごとに1つ以上の*ブートエントリ*から構成されます。

    *ブートエントリ*は、オペレーティングシステムまたは起動可能なプログラムの負荷構成を定義する一連のオプションです。 ブートエントリでは、オペレーティングシステムまたは起動可能なプログラムとそのファイルの場所を指定します。 また、オペレーティングシステムまたはプログラムを構成するパラメーターを含めることもできます。

    次のサンプルは、Microsoft Windows XP と Microsoft Windows 2000 の2つのオペレーティングシステムが搭載されたコンピューターの boot.ini の \[オペレーティングシステム\] セクションを示しています。 これには、オペレーティングシステムごとに1つずつ、2つのブートエントリがあります。

    ```
    [operating systems]
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
    multi(0)disk(0)rdisk(0)partition(2)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
    ```

各ブートエントリには、次の要素が含まれています。

-   オペレーティングシステムの場所。 Boot.ini では、Advanced RISC Computing (ARC) 名前付け規則を使用して、オペレーティングシステムが存在するディスクパーティションとディレクトリへのパスを表示します。 次に、例を示します。
    ```
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   ブートエントリのフレンドリ名。 フレンドリ名は、ブートメニューのブートエントリを表します。 フレンドリ名は引用符で囲まれ、ブートメニューのブートエントリを表します。 次に、例を示します。
    ```
    "Microsoft Windows XP Professional"
    ```

-   *ブートエントリパラメーター*。*ブートパラメーター*または*読み込みオプション*とも呼ばれ、オペレーティングシステムの機能を有効化、無効化、および構成します。 ブートパラメーターは、コマンドラインパラメーターと似ています。各パラメーターは、 [ **/debug**](https://docs.microsoft.com/windows-hardware/drivers/devtest/-debug)のようにスラッシュ (/) で始まります。 ブートエントリごとに、0個以上のブートパラメーターを設定できます。

    ドライバーのテストとデバッグに関連するブートパラメーターの一覧については、「boot.ini[ブートパラメーターリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

同じオペレーティングシステムに対して複数のブートエントリを持つことができ、それぞれに異なるブートパラメーターのセットがあります。 オペレーティングシステムをインストールすると、Windows によって標準のブートエントリが作成されます。また、Boot.ini を編集して、オペレーティングシステム用にカスタマイズされた追加のエントリを作成することもできます。
