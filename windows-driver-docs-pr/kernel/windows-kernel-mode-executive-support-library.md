---
title: Windows カーネル モードの経営陣の支持ライブラリ
description: Windows カーネル モードの経営陣の支持ライブラリ
ms.assetid: cfb8c6c0-9454-4dc6-98e8-c41cbf1c0cad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 86dbe8b256d2148fe6bdc7c28429f90cf8f9e782
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556793"
---
# <a name="windows-kernel-mode-executive-support-library"></a>Windows カーネル モードの経営陣の支持ライブラリ


Windows オペレーティング システムの使用、用語*executive レイヤー*にさまざまなサービスを含む、デバイス ドライバーを提供するカーネル モード コンポーネントを参照してください。

-   オブジェクトの管理

-   メモリ管理

-   プロセスおよびスレッド管理

-   入力/出力の管理

-   構成管理

上記のマネージャーは、いくつかのライブラリと同様、個々 のテクノロジに直接インターフェイスを提供します。 ただし、Executive ライブラリにジェネリック インターフェイスとして一緒にグループ化されているルーチンが、通常は付いて"**Ex**"、たとえば、 **ExGetCurrentResourceThread**します。 Executive ライブラリ ルーチンの一覧は、[Executive ライブラリ サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff544582)を参照してください。

ドライバーと HAL 含まれていないこと、経営層の経営層のコンポーネント、Ntoskrnl.exe の一部であることに注意してください。

 

 




