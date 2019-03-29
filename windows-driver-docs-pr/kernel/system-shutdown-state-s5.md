---
title: システム シャットダウン状態 S5
description: システム シャットダウン状態 S5
ms.assetid: c08d688d-c31a-4d57-a343-406edfa35e8f
keywords:
- S5 WDK 電源管理
- システム シャット ダウン状態 WDK 電源管理
- ソフトウェアの再開 WDK 電源管理
- WDK の電源管理の再開
- ハードウェアの遅延 WDK 電源管理
- システム ハードウェア コンテキスト WDK 電源管理
- ハードウェア コンテキスト WDK 電源管理
- WDK の電源管理のコンテキスト
- WDK の電源管理の待機時間
- システム電源の状態 WDK カーネル、シャット ダウン状態
- シャット ダウン状態 WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9df301c371a885e03170409c80cd05c1f63d8be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579026"
---
# <a name="system-shutdown-state-s5"></a>システム シャットダウン状態 S5





S5、またはシャット ダウン状態で、マシンはメモリの状態を保持しないと、計算タスクが実行されていません。

状態 S4 および S5 の唯一の違いは、状態 S5 から再起動は、システムの再起動が必要ですが、コンピューターを状態、S4 で休止状態ファイルから再起動できることです。

S5 状態では、次の特徴があります。

<a href="" id="power-consumption"></a>**電力消費量**  
オフ、以外の少量の電源ボタンなどのデバイスに現在します。

<a href="" id="software-resumption"></a>**ソフトウェアの再開**  
ブートは、アクティブ化時に必要があります。

<a href="" id="hardware-latency"></a>**ハードウェアの遅延**  
長いと未定義です。 ON スイッチを押すと、ユーザーなどの物理操作では、作業の状態にシステムを返します。 BIOS は、システムが構成されているため再開タイマーからも目覚めさせることができます。

<a href="" id="system-hardware-context"></a>**システム ハードウェアのコンテキスト**  
None は保持されます。

 

 




