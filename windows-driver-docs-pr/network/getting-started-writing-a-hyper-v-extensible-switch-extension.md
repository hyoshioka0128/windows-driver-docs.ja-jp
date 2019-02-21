---
title: 記述について、HYPER-V 拡張可能スイッチの拡張機能
description: このセクションは、HYPER-V 拡張可能スイッチの拡張機能の記述を開始する方法を説明します
ms.assetid: 91C6ED75-1057-4520-8E8E-28817D8F3C81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef7f91118982c0372ebf4ad28fd9845f8cdff05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527342"
---
# <a name="getting-started-writing-a-hyper-v-extensible-switch-extension"></a>記述について HYPER-V 拡張可能スイッチの拡張機能


HYPER-V 拡張可能スイッチの拡張機能は、NDIS フィルターです。 または、HYPER-V 拡張可能スイッチ (「HYPER-V 仮想スイッチ」とも呼ばれます) 内で実行される Windows フィルタ リング プラットフォーム (WFP) フィルターです。

拡張機能の 3 つのクラスがあります。 キャプチャ、フィルター、および転送します。 それらのすべては、NDIS フィルター ドライバーとして実装することができます。 フィルター拡張機能は、WFP フィルター ドライバーとして実装できます。

ドライバー開発者向けのアーキテクチャ概要については、次を参照してください。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)します。

HYPER-V 拡張可能スイッチの拡張機能を作成するには、次の手順を実行します。

1.  拡張機能のアーキテクチャとプログラミング モデルについて説明します。
    -   以降では、NDIS ベースの拡張は、オンライン ドキュメントを読み取る[HYPER-V 拡張可能スイッチ](hyper-v-extensible-switch.md)します。 キャプチャ、フィルター処理、および転送拡張機能を使用して、標準の NDIS API をフィルター処理します。 NDIS インターフェイスは、構成、通知、および仮想スイッチと仮想マシンの id を提供する拡張されています。
        [HYPER-V 拡張可能スイッチ関数](https://msdn.microsoft.com/library/windows/hardware/hh598171)
        [HYPER-V 拡張可能スイッチの列挙体](https://msdn.microsoft.com/library/windows/hardware/hh598168)
        [HYPER-V 拡張可能スイッチ構造体と共用体](https://msdn.microsoft.com/library/windows/hardware/hh598189)
         [HYPER-V 拡張可能スイッチ Oid](https://msdn.microsoft.com/library/windows/hardware/hh598178)
        [HYPER-V 拡張可能スイッチの状態インジケーター](https://msdn.microsoft.com/library/windows/hardware/hh598188)
        [HYPER-V 拡張可能スイッチ マクロ](https://msdn.microsoft.com/library/windows/hardware/hh598175)
    -   以降では、WFP ベースの拡張は、オンライン ドキュメントを読み取る[仮想スイッチを使用してフィルター](using-virtual-switch-filtering.md)します。
    -   拡張機能に次の説明ビデオをご覧ください。
        -   [HYPER-V 拡張可能スイッチの techEd セッション](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2012/VIR307)
        -   [Hyper V の拡張可能スイッチ、第 1 部-概要](http://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-I--Introduction)
        -   [HYPER-V 拡張可能スイッチ、パート II: コントロールのパスを理解します。](http://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-II--Understanding-the-Control-Path)
        -   [HYPER-V 拡張可能スイッチ、第 3 部-キャプチャおよびフィルターの拡張機能のデータパスの入出力](http://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-III--The-Ins-and-Outs-of-the-Data-Path-for-Capture-and-Filter-Extensi)
    -   拡張機能の管理に使用できるいくつかの PowerShell コマンドもあります。 これらは記載[管理インストールされている HYPER-V 拡張可能スイッチ拡張機能](managing-installed-hyper-v-extensions.md)します。

2.  開発環境を設定します。
    -   Microsoft Visual Studio Professional 2012 をインストールします。
    -   ダウンロードしてインストール[Windows Driver Kit 8](https://msdn.microsoft.com/library/windows/hardware/gg487428.aspx)します。

3.  サンプル拡張機能を学習します。
    -   ダウンロード、[転送拡張機能サンプルの NDIS](https://go.microsoft.com/fwlink/p/?LinkId=618935)します。
    -   ダウンロード、 [WFP サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618934)します。 これは、vSwitch 機能が含まれる機能のプロトタイプです。

4.  拡張機能を記述します。
    -   フィルター コードの既存のポートを開始点として、サンプルの 1 つを使用したり、拡張機能をゼロから作成できます。
    -   NDIS 拡張機能を開発する場合を使ってできます標準 NDIS INF いくつかの変更」の説明に従って[HYPER-V 拡張可能スイッチ拡張機能の要件を INF](inf-requirements-for-hyper-v-extensions.md)します。

5.  拡張機能のビルドと単体テスト。
    -   必要があります[Visual Studio を使用して、拡張機能を構築する](https://msdn.microsoft.com/library/windows/hardware/ff554644.aspx)します。
    -   できます理解しておく拡張機能のビルド プロセスでコンパイルしているサンプル拡張機能を実行する Visual Studio を使用します。

6.  署名済み拡張機能を取得するための Windows 認定 (ロゴ) プロセスについて説明します。
    -   拡張機能のテストを渡す必要があります、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)します。
    -   拡張機能の要件については、「で Filter.Driver.vSwitchExtension.ExtensionRequirements、 [Windows ハードウェア認定要件 - フィルター ドライバー](https://msdn.microsoft.com/library/windows/hardware/jj128255)します。

7.  Windows ハードウェア認定キット環境を設定します。
    -   ダウンロードしてインストール、 [Windows ハードウェア認定キット](https://msdn.microsoft.com/windows/hardware/hh852359)します。

8.  拡張機能の WHCK テストを実行します。
    -   Filter.Driver.Fundamentals
    -   Filter.Driver.Security
    -   Filter.Driver.vSwitchExtension

9.  WHCK 証明に合格する最終的な拡張機能と後に Microsoft に送信します。
    -   拡張機能を追跡できなどの管理のパッケージによってデプロイされることを確認する特定の形式での MSI インストール パッケージとして送信する必要があります[System Center Virtual Machine Manager (SCVMM) 2012](https://technet.microsoft.com/magazine/hh300651.aspx)します。 MSI の形式が定義されている[拡張ドライバー MSI パッケージ要件](https://msdn.microsoft.com/library/windows/hardware/hh921657.aspx)します。

10. WindowsServerCatalog.com で拡張機能の一覧を表示します。
    -   WindowsServerCatalog.com で拡張機能の簡単な説明を一覧表示します。
    -   WindowsServerCatalog.com で認定された拡張機能の一覧を表示する方法については、間もなく提供されます。

 

 





