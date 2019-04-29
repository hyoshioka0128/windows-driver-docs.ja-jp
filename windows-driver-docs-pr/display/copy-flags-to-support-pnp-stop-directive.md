---
title: PnP 停止ディレクティブをサポートするためのフラグをコピーする
description: プラグ アンド プレイ (PnP) 停止ディレクティブ ファイルのセクション フラグは、再起動を必要としないドライバーをアップグレードをサポートするために Windows Display Driver Model (WDDM) に必要です。
ms.assetid: 0D78350C-52D9-49D5-817D-2672F4A1D41A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f17147db56303194139b141f525e4c12935fee89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330634"
---
# <a name="copy-flags-to-support-pnp-stop-directive"></a>PnP 停止ディレクティブをサポートするためのフラグをコピーする


プラグ アンド プレイ (PnP) 停止ディレクティブ ファイルのセクション フラグは、再起動を必要としないドライバーをアップグレードをサポートするために Windows Display Driver Model (WDDM) に必要です。

**注**  これは、カーネル モード ドライバーのエントリではなく、ユーザー モード ドライバーのバイナリにのみ必要です。

 

例:

``` syntax
;
; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000             ; COPYFLG_IN_USE_TRY_RENAME
r200umd2.dll,,,0x00004000           ; COPYFLG_IN_USE_TRY_RENAME
```

 

 





