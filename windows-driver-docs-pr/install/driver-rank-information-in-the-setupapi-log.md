---
title: SetupAPI ログ ドライバーのランク付け情報
description: SetupAPI ログ ドライバーのランク付け情報
ms.assetid: 169a1963-3fb3-4254-9634-78034cda2924
keywords:
- SetupAPI WDK Windows Vista では、ドライバーのランク付け情報をログ記録
- 署名インジケーター WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a0583922123f50ba3b33c08e5f01eb5fe62402
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528486"
---
# <a name="driver-rank-information-in-the-setupapi-log"></a>SetupAPI ログ ドライバーのランク付け情報


Windows では、署名のインジケーターを使用して、署名の種類を表します。 Windows では、この情報の保存、[ドライバー ストア](driver-store.md)データベース内部で使用します。

SetupAPI が追加のドライバーをインストールすると、Windows、*ランク*ドライバーのランクを 16 進形式と署名の種類のログを署名者のスコアのエントリのログ エントリ。 太字のフォント スタイル、順位付けのエントリの例、および署名者のスコアのエントリの例で示す SetupAPI デバイス ログからの抜粋を次に示します。 この抜粋では、順位付けのエントリは、ドライバーは"0x0dff0000"のランクを署名者のスコアのエントリの場合、ドライバーが、受信トレイのドライバーであることを示しますを示します。

```cpp
     dvi:      Created Driver Node:
     dvi:           HardwareID   - ROOT\UPDATE
     dvi:           InfName      - D:\Windows\System32\DriverStore\FileRepository\machine.inf_36c3d8da\machine.inf
     dvi:           DevDesc      - Microcode Update Device
     dvi:           DrvDesc      - Microcode Update Device
     dvi:           Provider     - Microsoft
     dvi:           Mfg          - (Standard system devices)
     dvi:           InstallSec   - UPDATE_DRV
     dvi:           ActualSec    - UPDATE_DRV
     dvi:           Rank         - 0x0dff0000
     dvi:           Signer       - Microsoft Windows Component Publisher
     dvi:           Signer Score - INBOX
     dvi:           DrvDate      - 10/01/2002
     dvi:           Version      - 6.0.5270.8
```

Windows は、署名の種類ごとに SetupAPI デバイス ログに記録される署名者のスコアのエントリの一覧を次には。

<a href="" id="premium-whql-signature"></a>Premium WHQL 署名  
「署名者スコア - WHQL ロゴ Gold」

<a href="" id="standard-whql-signature"></a>標準の WHQL 署名  
「署名者スコア - WHQL ロゴ Silver」

<a href="" id="an-unspecified-microsoft-signature"></a>未指定のマイクロソフトの署名  
「署名者スコア - WHQL Unclassified」

<a href="" id="a-whql-signature-for-a-windows-version-earlier-than-windows-vista-and-equal-to-or-later-than-the-lowerlogoversion-value-of-the-driver-s-device-setup-class-"></a>Windows Vista より前と同じかより後の Windows バージョンについては、WHQL 署名、 [LowerLogoVersion](lowerlogoversion.md)ドライバーのデバイス セットアップ クラスの値。  
「署名者スコア - WHQL」

<a href="" id="a-microsoft-signature-for-an-inbox-driver"></a>受信トレイのドライバーの Microsoft の署名  
「署名者スコア - 受信トレイ」

<a href="" id="an-authenticode-signature-or-whql-signature-for-a-windows-version-earlier-than-the-version-that-is-specified-by-lowerlogoversion-for-the-device-setup-class-of-the-driver"></a>Authenticode 署名または WHQL 署名で指定されているバージョンよりも前の Windows バージョンを**LowerLogoVersion**ドライバーのデバイス セットアップ クラスに対する  
「署名者スコア - Authenticode」

<a href="" id="unsigned-driver"></a>署名されていないドライバー  
「署名者スコア - デジタル署名されていない」

ドライバーのランク付けの詳細については、次を参照してください。[どの Windows ランクのドライバー (Windows Vista 以降)](how-setup-ranks-drivers--windows-vista-and-later-.md)します。

 

 





