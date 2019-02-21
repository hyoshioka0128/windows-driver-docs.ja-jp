---
title: メディアの検証
description: メディアの検証
ms.assetid: 609ac09b-88be-49a6-8b87-9fd453c21446
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルは、WDK のファイル システム、メディアの検証を確認します。
- メディアの検証の WDK ファイル システム
- 死のディスクは、WDK のファイル システムを攻撃します。
- WDK のファイル システムのメディアの検証
- リムーバブル メディアの検証の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d36445f9fc02dc36ddfecd2db26ed2dc5b269e90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548811"
---
# <a name="media-validation"></a>メディアの検証


## <span id="ddk_media_validation_if"></span><span id="DDK_MEDIA_VALIDATION_IF"></span>


リムーバブル メディア (たとえば FASTFAT) をサポートするファイル システムを開発するときに、大きな問題は、「死のディスク」攻撃から保護するため。 リムーバブル ディスクを挿入できるすべてのユーザーからファイル システムを実装する場合、ドライバーが悪意のある形式が正しくない構造体に対して防ぐ必要があります (CD-ROM、DVD-ROM、または USB メモリのディスクをフラッシュなど)、システムにします。

 

 




