---
title: PnP 停止ディレクティブをサポートするためにフラグをコピーします。
description: プラグ アンド プレイ (PnP) 停止ディレクティブ ファイルのセクション フラグは、再起動を必要としないドライバーをアップグレードをサポートするために Windows Display Driver Model (WDDM) に必要です。
ms.assetid: 0D78350C-52D9-49D5-817D-2672F4A1D41A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f17147db56303194139b141f525e4c12935fee89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539227"
---
# <a name="copy-flags-to-support-pnp-stop-directive"></a>PnP 停止ディレクティブをサポートするためにフラグをコピーします。


プラグ アンド プレイ (PnP) 停止ディレクティブ ファイルのセクション フラグは、再起動を必要としないドライバーをアップグレードをサポートするために Windows Display Driver Model (WDDM) に必要です。

**注**  これは、カーネル モード ドライバーのエントリではなく、ユーザー モード ドライバーのバイナリにのみ必要です。

 

次に、例を示します。

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

 

 





