---
title: Windows カーネル モードのカーネル ライブラリ
description: Windows カーネル モードのカーネル ライブラリ
ms.assetid: e62264ee-5d52-4ae1-bd54-51e93c34762f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 45bd22b0bd5b4ff743fcf9f73d4e38e7b8d37e23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529945"
---
# <a name="windows-kernel-mode-kernel-library"></a>Windows カーネル モードのカーネル ライブラリ


*カーネル*オペレーティング システムのオペレーティング システムで他のすべてが依存するコア機能を実装します。 Microsoft Windows カーネルでは、スレッドのスケジューリングやルーティング ハードウェア割り込みなどの基本的な低レベル操作を提供します。 オペレーティング システムの中核を実行するすべてのタスクが高速で単純にする必要があります。

カーネル ライブラリへの直接のインターフェイスを提供するルーチンが、通常は付いて"**Ke**"、たとえば、 **KeGetCurrentThread**します。 カーネル ライブラリ ルーチンの一覧は、次を参照してください。[カーネル ライブラリ サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff542078)します。

**注**  用語*マイクロ カーネル*Windows オペレーティング システムで使用される現在のカーネルには適用されません。

 

 

 




