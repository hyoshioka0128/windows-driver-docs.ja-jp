---
title: PnP 停止をサポートするためのファイル コピー フラグの設定
description: PnP 停止をサポートするためのファイル コピー フラグの設定
ms.assetid: 9f716ac0-c181-489f-8bc4-ccca8c141b06
keywords:
- INF ファイルを WDK の表示、コピー ファイル フラグ
- ファイルのコピー フラグ WDK の表示
- PnP 停止 WDK の表示
- プラグ アンド プレイ停止 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7d9995e934a29dfe3a7078bdac289963a91d74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390468"
---
# <a name="setting-a-copy-file-flag-to-support-pnp-stop"></a>PnP 停止をサポートするためのファイル コピー フラグの設定


新しいファイルのコピーのフラグは、ディスプレイ ドライバー プラグ アンド プレイ (PnP) 停止 (つまり、システムの再起動を必要としないドライバー アップグレード) を正しくサポートするために Windows 表示 Driver Model (WDDM) に書き込まれる必要があります。

**注**  このフラグは、ユーザー モードのディスプレイ ドライバーのバイナリおよびディスプレイのミニポート ドライバーではなく必要です。

 

ユーザー モードのファイルのコピー セクションでは単に追加される新しいファイルのコピーのフラグがドライバーを表示し、ミニポート ドライバーを表示しないは、次の例です。

```cpp
;
; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000  ; COPYFLG_IN_USE_TRY_RENAME
r200umd2.dll,,,0x00004000 ; COPYFLG_IN_USE_TRY_RENAME
```

詳細については、 **CopyFiles**ディレクティブとファイルのセクションでは関連付けられている**CopyFiles**を参照してください[ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346).

 

 





