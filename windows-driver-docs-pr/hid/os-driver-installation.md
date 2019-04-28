---
title: OS ドライバーのインストール
description: 仕入先が、Microsoft 提供のキーボードとマウス クラスのインストーラーを制御するために使用できるクラス固有 INF ファイルのエントリは、デバイスをインストールします。
ms.assetid: A934B1F3-01FA-4B70-92B8-9CB3EB096C89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d263ab4caaff3a32583d1b22051cc6e05c43affb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372967"
---
# <a name="os-driver-installation"></a>OS ドライバーのインストール


ここでは、仕入先は、Microsoft 提供のキーボードとマウス クラスのインストーラーが Microsoft Windows 2000 以降でデバイスをインストールする方法を制御に使用できる次のクラスに固有 INF ファイル エントリを説明します。

:

[INF DDInstall.MigrateToDevNode セクション](inf-ddinstall-migratetodevnode-section.md)

[INF SharedDriver エントリ](inf-shareddriver-entry.md)

[INF PS2\_Inst.NoInterruptInit.Bioses セクション](inf-ps2-inst-nointerruptinit-bioses-section.md)

[INF PS2\_Inst.NoInterruptInit セクション](inf-ps2-inst-nointerruptinit-section.md)

具体的な例については、これらの INF ファイル エントリ keyboard.inf と msmouse.inf--のキーボードとマウス デバイス セットアップ クラスに対する Microsoft 提供の INF ファイルでの使用状況を参照してください。

## <a name="general-rules-for-ps2-keyboards-and-mice"></a>Ps/2 キーボードとマウスの一般的な規則


すべての内部/統合デバイス PS/2 と互換性のあるコント ローラーを介して接続されている、Microsoft Windows オペレーティング システムは、デバイスのデバイスの識別文字列のリストの構築に ACPI を使用します。 プラグ アンド プレイ マネージャーでは、これらのデバイスの識別文字列を使用して、INF ファイルにデバイスを照合します。 プラグ アンド プレイ デバイス文字列は、次の種類に分類されます。

-   1 つ一意のデバイス ID (だけ多くの場合は、ハードウェア Id の一覧での最初の ID)
-   ハードウェア Id の順序付きリスト
-   互換性 Id の順序付きリスト

プラグ アンド プレイ Manager 常に識別子を使用してすべての一覧で INF ファイルでは、デバイスの一致を試みますが、最初に最も固有の識別子を使用しようとします。 これにより、優先度リストの一番上にベンダーによって提供されるこれらのドライバーとの適合性、順序のドライバーを優先するためのセットアップ ソフトウェアです。

一致するドライバーを見つけるには、セットアップは、デバイスのハードウェア Id を比較し、ハードウェア Id および互換性 Id に、互換性 Id (デバイスの親のバス ドライバーによって報告される) と、コンピューター上の INF ファイルに記載します。 セットアップには、1 つ以上の一致が検出されると、各ドライバーの一致に"rank"が割り当てられます。 ランク番号が低いほど、デバイスのドライバーより適合します。

上記のシナリオを実現するために ACPI を次にレポートする必要があります。

1 つまたは複数のファームウェアとハードウェアのモデルを識別するためにハードウェア Id。 (仕様で定義されて ACPI V5.0) HWID の形式は次のとおりです。

-   ACPI\\VEN\_vvvv & DEV\_dddd & SUBSYS\_ssssssss & REV\_rrrr
-   ACPI\\VEN\_vvvv & DEV\_dddd & SUBSYS\_ssssssss
-   ACPI\\VEN\_vvvv & DEV\_dddd & REV\_rrrr
-   ACPI\\VEN\_vvvv & DEV\_dddd & CLS\_cccc & SUBCLS\_nnnn & PI\_pp
-   ACPI\\VEN\_vvvv & DEV\_dddd
-   ACPI\\vvvdddd
-   ACPI\\vvvvdddd

ジェネリック クラス ドライバーの読み込みにオペレーティング システムに互換性のある 1 つの ID。 これらの汎用的な Id は、キーボードとマウスの Inf に既に表示されています。

Ps/2 キーボード ハードウェア id が正しく書式設定されたシステムの例は次のとおりです。

-   ハードウェア ID:ACPI\\MSF0001;
-   互換性のある ID:\*PNP0303

注:

-   Windows では、ACPI ハードウェア Id をレガシ (ACPI 4.0 など) のスタイルにできますが、固有のキーボードまたはマウス デバイスを常に特定したことが優先されます。
-   Windows ハードウェア認定キットには、次の要件 (System.Fundamentals.Input.PS2UniqueHWID) が含まれています。 Ps/2 経由でモバイル コンピューティングの要素にキーボードとマウスを埋め込み、システム製造元が一意なハードウェア ID を確認する必要があります。 一意のハードウェア ID は、デバイスを識別し、適切なドライバーをロードします Windows Update (WU) を許可する形式である必要があります。 この Windows 8 ロゴの要件がモバイル x86/64 システムはサポートされません ps/2 ARM システム) に適用されます。

詳細については、"ラップトップ上の ps/2 入力デバイスのハードウェア Id に「MSDN ホワイト ペーパーを参照してください。

 

 




