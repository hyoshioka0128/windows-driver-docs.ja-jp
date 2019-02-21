---
title: ドライバーでは、レジストリを使用します。
description: ドライバーでは、レジストリを使用します。
ms.assetid: 69d2d491-3cc1-4fd0-a1c9-0cc8e73e69b2
keywords:
- レジストリの WDK カーネル
- ドライバーのレジストリ情報の WDK カーネル
- 記憶域の WDK レジストリ
- レジストリ情報を格納します。
- ドライバーのレジストリに関する、レジストリの WDK カーネル
- ドライバー レジストリ情報 WDK カーネル ドライバーのレジストリについて
- レジストリ エントリの WDK カーネルを操作します。
- WDK カーネル レジストリのキー
- WDK カーネル レジストリのサブキー
- カーネル モード ドライバー WDK、レジストリ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 738699c9c45539aac64cd9b468c6826d6c78220b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551158"
---
# <a name="using-the-registry-in-a-driver"></a>ドライバーでは、レジストリを使用します。





その他のシステム コンポーネントと同様に、ドライバーは、構成情報を格納するレジストリに依存します。 システム自体が、レジストリを使用してデバイスおよびドライバーに関する情報を格納し、ドライバーを使用して独自の追加情報がありますを格納できます。

Microsoft Windows の役員は、レジストリを操作する次の 2 つのルーチンのセットを提供します。

[レジストリ キー オブジェクトのルーチン](registry-key-object-routines.md)

[レジストリのランタイム ライブラリ ルーチン](registry-run-time-library-routines.md)

[プラグ アンド プレイ レジストリ ルーチン](plug-and-play-registry-routines.md)

詳細については、レジストリを参照してください。

[**INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[ドライバーのレジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff549538)

 

 




