---
title: Windows カーネルモード カーネル ライブラリ
description: Windows カーネルモード カーネル ライブラリ
ms.assetid: e62264ee-5d52-4ae1-bd54-51e93c34762f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4483335a8fc50525563d386a5b4324f43c6a0f5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357980"
---
# <a name="windows-kernel-mode-kernel-library"></a>Windows カーネルモード カーネル ライブラリ


*カーネル*オペレーティング システムのオペレーティング システムで他のすべてが依存するコア機能を実装します。 Microsoft Windows カーネルでは、スレッドのスケジューリングやルーティング ハードウェア割り込みなどの基本的な低レベル操作を提供します。 オペレーティング システムの中核を実行するすべてのタスクが高速で単純にする必要があります。

カーネル ライブラリへの直接のインターフェイスを提供するルーチンが、通常は付いて"**Ke**"、たとえば、 **KeGetCurrentThread**します。 カーネル ライブラリ ルーチンの一覧は、次を参照してください。[カーネル ライブラリ サポート ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff542078(v=vs.85))します。

**注**  用語*マイクロ カーネル*Windows オペレーティング システムで使用される現在のカーネルには適用されません。

 

 

 




