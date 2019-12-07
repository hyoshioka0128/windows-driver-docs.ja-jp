---
title: Windows カーネルモード エグゼクティブ サポート ライブラリ
description: Windows カーネルモード エグゼクティブ サポート ライブラリ
ms.assetid: cfb8c6c0-9454-4dc6-98e8-c41cbf1c0cad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 634071d735ed22581a50eed20b47e516ad604f5a
ms.sourcegitcommit: a97a623d64ddf573c760664be17778606e156cf5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74907121"
---
# <a name="windows-kernel-mode-executive-support-library"></a>Windows カーネルモード エグゼクティブ サポート ライブラリ


Windows オペレーティングシステムでは、 *executive レイヤー*という用語を使用して、デバイスドライバーに対してさまざまなサービスを提供するカーネルモードコンポーネントを参照します。これには次のものが含まれます。

-   オブジェクト管理

-   メモリ管理

-   プロセスとスレッドの管理

-   入出力管理

-   構成管理

これらの各マネージャーは、複数のライブラリを使用して、個々のテクノロジに直接インターフェイスを提供します。 ただし、Executive ライブラリへの汎用インターフェイスとしてグループ化されたルーチンには、通常、"**Ex**" (たとえば、 **Exgetcurrentresourcethread**) というプレフィックスが付いています。 Executive ライブラリルーチンの一覧については、「 [Executive Library Support ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/#executive-library-support-routines)」を参照してください。

Executive レイヤーコンポーネントは、Ntoskrnl.exe に含まれていますが、そのドライバーと HAL は、executive レイヤーの一部ではないことに注意してください。

 

 




