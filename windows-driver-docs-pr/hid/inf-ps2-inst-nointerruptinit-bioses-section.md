---
title: INF PS2_Inst.NoInterruptInit.Bioses セクション
description: INF PS2_Inst.NoInterruptInit.Bioses セクション
ms.assetid: 2bf1dc0f-00b6-4f4a-99f0-e9843fe6e66b
keywords:
- INF ファイル WDK 非 HID キーボード/マウス
- PS2_Inst.NoInterruptInit.Bioses セクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7c36898c220502cac53e641a2b47225d719393a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551493"
---
# <a name="inf-ps2instnointerruptinitbioses-section"></a>INF PS2\_Inst.NoInterruptInit.Bioses セクション





**\[PS2\_Inst.NoInterruptInit.Bioses\]**

*無効にする*=*無効にする文字列*マウス クラスのインストーラーが場合にチェック d*無効にする文字列*の文字列値の部分文字列は、 **HKLM\\ハードウェア\\説明\\システム\\SystemBiosVersion**します。 クラスのインストーラーがで指定した INF ディレクティブを実行する場合は、 [INF PS2\_Inst.NoInterruptInit セクション](inf-ps2-inst-nointerruptinit-section.md)します。

### <a name="entries-and-values"></a>エントリと値

<a href="" id="disable"></a>*無効にします。*  
D に設定*無効にする文字列*値。

<a href="" id="disable-string"></a>*無効にする文字列*  
内の部分文字列を指定します**HKLM\\ハードウェア\\説明\\システム\\SystemBiosVersion**をシステム BIOS を一意に識別します。

### <a href="" id="comments"></a>「解説」

Ps/2 マウス デバイスでのみとの組み合わせでのみこのセクションを使用して、 [INF **PS2\_Inst.NoInterruptInit**セクション](inf-ps2-inst-nointerruptinit-section.md)します。

 

 




