---
title: Hyper-v 拡張可能スイッチ拡張機能の作成の概要
description: このセクションでは、Hyper-v 拡張可能スイッチ拡張機能の記述を開始する方法について説明します。
ms.assetid: 91C6ED75-1057-4520-8E8E-28817D8F3C81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfcebe72493e14faaa821e4d39e619816146104a
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256762"
---
# <a name="getting-started-writing-a-hyper-v-extensible-switch-extension"></a>Hyper-V 拡張可能スイッチ拡張機能の作成の開始

Hyper-v 拡張可能スイッチ拡張機能は、Hyper-v 拡張可能スイッチ ("Hyper-v 仮想スイッチ" とも呼ばれます) の内部で実行される NDIS フィルターまたは Windows フィルタリングプラットフォーム (WFP) フィルターです。

拡張機能には、キャプチャ、フィルター処理、転送という3つのクラスがあります。 これらはすべて、NDIS フィルタードライバーとして実装できます。 フィルター拡張機能は、WFP フィルタードライバーとして実装することもできます。

ドライバー開発者向けのアーキテクチャの概要については、「 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)」を参照してください。

Hyper-v 拡張可能スイッチ拡張機能を作成するには、次の手順を実行します。

1. 拡張機能のアーキテクチャとプログラミングモデルについて説明します。
    -   詳細については、「 [hyper-v 拡張可能スイッチ](hyper-v-extensible-switch.md)」を参照してください。 拡張機能のキャプチャ、フィルター処理、転送には、標準の NDIS フィルター API が使用されます。 NDIS インターフェイスは、仮想スイッチと仮想マシンの構成、通知、および id を提供するように強化されています。
        Hyper-v 拡張可能スイッチの[関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
        hyper-v 拡張可能スイッチの[列挙](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)体
        hyper-v 拡張可能スイッチ[の構造と共用体](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
        hyper-v 拡張可能スイッチの[oid](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-oids)を
        hyper-v 拡張可能スイッチの[状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-status-indications)を示す
        [hyper-v 拡張可能](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-macros)スイッチのマクロ
    -   [仮想スイッチのフィルター処理を使用し](using-virtual-switch-filtering.md)た後に、WFP ベースの拡張機能に関するオンラインドキュメントを参照してください。
    -   拡張機能については、次の説明ビデオをご覧ください。
        -   [Hyper-v 拡張可能スイッチでの TechEd セッション](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2012/VIR307)
        -   [Hyper-v 拡張可能スイッチ、パート I-概要](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-I--Introduction)
        -   [Hyper-v 拡張可能スイッチパート II —制御パスを理解する](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-II--Understanding-the-Control-Path)
        -   [Hyper-v 拡張可能スイッチパート III —キャプチャとフィルター拡張機能のデータパスの入出力](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-III--The-Ins-and-Outs-of-the-Data-Path-for-Capture-and-Filter-Extensi)
    -   拡張機能の管理に使用できる PowerShell コマンドがいくつかあります。 これらは、「[インストール済みの Hyper-v 拡張可能スイッチ拡張機能の管理](managing-installed-hyper-v-extensions.md)」に記載されています。

2.  開発環境を設定する。
    -   Microsoft Visual Studio Professional をインストールします。
    -   [Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)をダウンロードしてインストールします。

3.  サンプルの拡張機能を調べます。
    -   [NDIS 転送拡張機能のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618935)をダウンロードします。
    -   [WFP サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618934)をダウンロードします。 これは、vSwitch 機能を含む機能しているプロトタイプです。

4.  拡張機能を作成します。
    -   いずれかのサンプルを開始点として使用するか、既存のフィルターコードを移植するか、拡張機能を最初から作成します。
    -   NDIS 拡張機能を開発している場合は、「 [Hyper-v 拡張可能スイッチ拡張機能の INF 要件](inf-requirements-for-hyper-v-extensions.md)」で説明されているように、標準の NDIS INF をいくつかの変更と共に使用できます。

5.  拡張機能をビルドし、単体テストを行います。
    -   [拡張機能をビルドするには、Visual Studio を使用](https://visualstudio.microsoft.com/vs/)する必要があります。
    -   拡張機能のビルドプロセスを理解するには、Visual Studio を使用してサンプルの拡張機能をコンパイルして実行します。

6.  拡張機能の署名を取得するための Windows 認定 (ロゴ) プロセスについて説明します。
    -   拡張機能は、 [Windows ハードウェア認定キット (HCK)](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/)のテストに合格する必要があります。
    -   拡張機能の要件については、「 [Windows ハードウェア認定の要件-フィルタードライバー](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/windows-hardware-certification-requirements---filter-driver) 」の「Driver. Vswitchextension. extensionrequirements 要件」に記載されています。

7.  Windows ハードウェア認定キット環境をセットアップします。
    -   [Windows ハードウェア認定キット](https://msdn.microsoft.com/windows/hardware/hh852359)をダウンロードしてインストールします。

8.  拡張機能のテストを実行します。
    -   フィルター. ドライバーの基礎
    -   フィルター. Driver. Security
    -   Driver. vSwitchExtension

9.  最終的な拡張機能が証明書に合格したら、Microsoft に送信します。
    -   拡張機能は、 [System Center Virtual Machine Manager (SCVMM) 2012](https://docs.microsoft.com/previous-versions/technet-magazine/hh300651(v=msdn.10))などの管理パッケージで追跡および展開できるように、特定の形式の MSI インストールパッケージとして提出する必要があります。 MSI 形式は、[拡張機能ドライバーの Msi パッケージ要件](https://docs.microsoft.com/windows-hardware/drivers/network/extension-driver-msi-packaging-requirements)で定義されています。

10. WindowsServerCatalog.com で拡張機能を一覧表示します。
    -   WindowsServerCatalog.com の拡張機能の簡単な説明を一覧表示します。
    -   認定された拡張機能を WindowsServerCatalog.com に掲載するための情報は、間もなく提供される予定です。
