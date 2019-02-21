---
title: WDDM 1.2 のベスト プラクティス
description: Windows では Windows 8 以降の最適なエクスペリエンスを提供するには、Windows Display Driver Model (WDDM) 1.2 またはそれ以降のドライバーとペアになっているグラフィックス ハードウェアが活用します。 このセクションでは、ベスト プラクティスをまとめたものです。
ms.assetid: 130C66F0-1ACE-4C6E-AE16-AEFCD4847312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5779f57d3a346fd6cb0e0c9df562cea5c769d75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549761"
---
# <a name="wddm-12-best-practices"></a>WDDM 1.2 のベスト プラクティス


Windows では Windows 8 以降の最適なエクスペリエンスを提供するには、Windows Display Driver Model (WDDM) 1.2 またはそれ以降のドライバーとペアになっているグラフィックス ハードウェアが活用します。 このセクションでは、ベスト プラクティスをまとめたものです。

**システム製造元:**

-   次の場合、十分にテストし、システムの構成で適切に動作を確認します。
    -   Microsoft Basic ディスプレイ ドライバーと互換性があります。
    -   再起動が必要ないサーバーの更新プログラム
-   WDDM ハードウェアで新しいサーバーを設計し、お客様のニーズに最適な関連する WDDM ドライバーの種類を採用します。
-   検証および WDDM 1.2 ドライバーの認定を取得するグラフィックス ハードウェアのベンダーと連携します。
-   ヘッドレス システム。
    -   システム ファームウェアは、IAPC で存在してしない VGA フラグを設定する必要があります\_ブート\_ARCH フィールド固定 ACPI 説明テーブル (FADT) は、空のモード一覧 VESA BIOS 拡張 (VBE) を通じてを実装する必要がありますすべて VBIOS がある場合。
    -   VBE のサポートがない場合は、ヘッドレス システムする必要があります作業表示 Unified Extensible Firmware Interface (UEFI) グラフィックス出力プロトコル (GOP) を通じてを表していません。
-   参照してください[Windows ハードウェア認定](https://go.microsoft.com/fwlink/p/?linkid=325510)の検証とテスト情報。
-   さまざまなデスクトップおよび Windows 8 以降では、solid のエンド ユーザー エクスペリエンスを確実にモバイル システムの両方のハードウェア構成をテストします。

**グラフィックス ハードウェア ベンダー:**

-   WDDM 1.2 ドライバーの開発を Microsoft と連携します。
-   Windows 8 以降のプレリリース版の WDDM 1.2 ドライバーをテストします。
-   Windows 更新プログラムによるデプロイ WDDM 1.x ドライバーの更新を Microsoft に提供します。
-   Windows 認定のテスト スイートに加え、グラフィックスとゲームのパフォーマンス、アプリケーションの互換性、および ASIC 各ファミリで、自己ホストのさまざまなシナリオを検証します。
-   WDDM 1.0 と 1.1 のドライバーが Windows 8 以降でテストします。
-   完全な製品のパッケージおよび WDDM 1.2 ドライバーを使用できるようにできるだけ早い段階です。

**独立系ソフトウェア ベンダー (Isv):**

-   Windows 8 以降、および WDDM 1.2 ドライバーでの既存および今後の Microsoft DirectX ゲームをテストします。
-   Windows 8 以降で個々 のアプリケーションをテストします。
-   Windows 8 の DirectX の拡張機能の活用します。

 

 





