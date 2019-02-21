---
title: Microsoft Basic ディスプレイ ドライバー
description: Windows 8 では、「Microsoft 基本的な表示ドライバー (MSBDD) は、XDDM VGA の保存と VGA PnP ドライバーを置換するボックスに表示ドライバーです。
ms.assetid: CE89E02E-6527-4285-998B-618EE235CB8F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44770f53929f205f3a27915af8df440cefd5cd59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530409"
---
# <a name="microsoft-basic-display-driver"></a>Microsoft Basic ディスプレイ ドライバー


Windows 8 では、「Microsoft 基本的な表示ドライバー (MSBDD) は、XDDM VGA の保存と VGA PnP ドライバーを置換するボックスに表示ドライバーです。

MSBDD を使用する主な利点は次のとおりです。

-   MSBDD により、一貫性のあるエンドユーザーを有効にして、開発者のエクスペリエンスを DirectX Api とデスクトップ コンポジションなどのテクノロジとの互換性があるためです。
-   サーバーのシナリオは、WDDM ドライバー モデルによって提供される高機能 (具体的には、再起動なしの更新プログラム、動的な開始と停止などの機能) を利用できます。
-   MSBDD には、Unified Extensible Firmware Interface (UEFI) グラフィックス出力プロトコル (GOP) がサポートされています。
-   MSBDD は XDDM と WDDM の両方のハードウェアで機能します。

MSBDD は、IHV グラフィック ドライバーがない場合、セーフ モードでのセットアップ中に読み込まれ、または、受信トレイに IHV のグラフィック ドライバーがインストールされている場合は、既定でボックスの表示のドライバーが動作していないまたは無効にします。 このドライバーの主な目的は、表示コント ローラーの線形フレーム バッファーに書き込む Windows です。

MSBDD は、モードと 1 つのモニターの解像度を管理するのにビデオの BIOS を使用できます。 UEFI のプラットフォームで MSBDD がブート中に設定されている線形フレーム バッファーを継承します。この場合、解像度やモードの変更を可能はありません。 ように*Microsoft 基本的なディスプレイ ドライバーによってサポートされている図 1 シナリオ*MSBDD は、次のシナリオで使用されます。

-   サーバー: WDDM 対応のグラフィックス ハードウェアのないサーバーの構成には、MSBDD を使用できます。
-   Windows のセットアップ:最後のブートの直前に、Windows セットアップの初期の段階では、MSBDD のみが読み込まれます。

    たとえば、ユーザーは、インボックス グラフィックス ドライバーの Windows 8 のサポートを持ちませんが、正常な状態になっている以前のプラットフォームを持ちます。 ユーザーが Windows 8 にアップグレードし、セットアップでは、インストール、MSBDD を使用し、IHV を取得する場合は、1 つのドライバーが使用可能です。

-   ドライバーのインストールで、次の場合:
    -   ユーザーが新しい IHV の WDDM ドライバーをインストールするとき、MSBDD は (新しい IHV ドライバーをインストールする前に、ポイントに古い IHV の WDDM ドライバーをアンインストールするとポイント) からの移行中に使用されます。
    -   ユーザーには、WDDM IHV の最新のドライバーのインストールに問題が検出されると、ユーザーまたはシステムを無効にできます、現在のグラフィックス ドライバーと MSBDD の使用にフォールバックします。
-   ドライバーのアップグレード:MSBDD を使用すると、IHV 推奨ドライバーにアップグレードするときに、システムの再起動を経由する必要はありません。
-   セーフ モード:このモードでは、信頼済みのドライバーのみが読み込まれます。これには、MSBDD が含まれます。

![microsoft の基本的なディスプレイ ドライバーによってサポートされるシナリオ](images/scenariossupportedmicrosoftbasicdisplaydriver.jpg)

**Microsoft Basic ディスプレイ ドライバーによってサポートされている図 1 のシナリオ**

 

 





