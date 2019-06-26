---
title: ドライバーでのレジストリの使用
description: ドライバーでのレジストリの使用
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
ms.openlocfilehash: dfd2c4b76825a7ff36259e7f0a9a44644bfa4734
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358168"
---
# <a name="using-the-registry-in-a-driver"></a>ドライバーでのレジストリの使用





その他のシステム コンポーネントと同様に、ドライバーは、構成情報を格納するレジストリに依存します。 システム自体が、レジストリを使用してデバイスおよびドライバーに関する情報を格納し、ドライバーを使用して独自の追加情報がありますを格納できます。

Microsoft Windows の役員は、レジストリを操作する次の 2 つのルーチンのセットを提供します。

[レジストリ キー オブジェクトのルーチン](registry-key-object-routines.md)

[レジストリのランタイム ライブラリ ルーチン](registry-run-time-library-routines.md)

[プラグ アンド プレイ レジストリ ルーチン](plug-and-play-registry-routines.md)

詳細については、レジストリを参照してください。

[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[ドライバーのレジストリ キー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)

 

 




