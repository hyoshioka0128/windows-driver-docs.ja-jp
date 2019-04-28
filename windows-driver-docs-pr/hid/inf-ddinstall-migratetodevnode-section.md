---
title: INF DDInstall.MigrateToDevNode セクション
description: INF DDInstall.MigrateToDevNode セクション
ms.assetid: a4edbc9e-a2d0-4012-aca9-0b357939a881
keywords:
- INF ファイル WDK 非 HID キーボード/マウス
- DDInstall.MigrateToDevNode セクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b60af77d117b1b7c9c21923a982da6f25cef7be9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364678"
---
# <a name="inf-ddinstallmigratetodevnode-section"></a>INF DDInstall.MigrateToDevNode セクション





**\[**<em>インストール セクション名</em>**します。MigrateToDevNode\]** |
**\[**<em>インストール セクション名</em>**.nt します。MigrateToDevNode\]** |
**\[**<em>インストール セクション名</em>**.ntx86 します。MigrateToDevNode\]** |
**\[**<em>インストール セクション名</em>**.ntia64 します。MigrateToDevNode\]**

<em>ServiceName</em>**=**<em>値名</em>\[**、**<em>値名</em>\]、.キーボードとマウスのクラスのインストーラーの一覧で指定されたエントリの値をコピーする*値名*レジストリ キーから文字列**HKLM\\システム\\CurrentControlSet\\サービス\\**<em>ServiceName</em>**\\パラメーター**インストールされているデバイスのデバイス ノードにします。

### <a name="entries-and-values"></a>エントリと値

<a href="" id="servicename"></a>*サービス名*  
デバイスのポートに関連付けられたサービス名を指定します (たとえば、 **i8042prt**、 **sermouse**など)。

<a href="" id="value-name"></a>*値の名前*  
レジストリ キーの下のエントリの値を指定します**HKLM\\システム\\CurrentControlSet\\サービス\\**<em>ServiceName</em> **\\パラメーター**します。

### <a href="" id="comments"></a>「解説」

Microsoft サポート INF <em>DDinstall</em>**します。MigratetoDevNode**セクションでは主に移植の Windows NT 4.0 従来のデバイスを Windows 2000 以降を容易にします。

キーボードとマウスのクラスのインストーラーは、すべてをコピー、*値名*エントリ値をシステムは、デバイス スタックを開始する前にします。 指定したエントリの値は、任意の有効なレジストリ エントリの値を指定できます。 *値名*エントリの値はから削除されず、 **.\\**  <em>ServiceName</em>**\\パラメーター**レジストリ キー。

 

 




