---
title: テープ ドライバー
description: テープ ドライバー
ms.assetid: d6d8ac92-0713-401c-9551-fc8e08e903f4
keywords:
- テープ ドライバー WDK ストレージ
- テープ記憶装置ドライバー WDK
- ストレージ ドライバー WDK、テープ ドライバー
- テープ ドライバー WDK ストレージ、テープ ドライバーについて
- テープ ドライバーに関するテープ ドライバー WDK、ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 675b243123df0199db857a1291f9a3d975befe84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386807"
---
# <a name="tape-drivers"></a>テープ ドライバー


## <span id="ddk_tape_drivers_kg"></span><span id="DDK_TAPE_DRIVERS_KG"></span>


このセクションには、次の情報が含まれています。

[テープのクラス ドライバーを使用してください。](using-the-tape-class-driver.md)

[必須および省略可能なテープ Miniclass ルーチン](required-and-optional-tape-miniclass-routines.md)

[省略可能な拡張機能でテープ Miniclass コンテキストを格納します。](storing-tape-miniclass-context-in-optional-extensions.md)

[テープ デバイスのコントロール要求を処理](processing-tape-device-control-requests.md)

NT ベースのオペレーティング システムでは、オペレーティング システムに固有とデバイスに依存しないテープのタスクを処理する汎用的なテープ クラス ドライバーを提供します。 テープのクラス ドライバーは、カーネル モード DLL として提供されます。 新しいテープ デバイスまたはテープ デバイスのファミリをサポートするには、ドライバー開発者はシステムが指定したテープのクラス ドライバーに動的にリンクしているデバイスに固有のテープ miniclass ドライバーを作成します。

テープ miniclass ドライバーは、テープ クラス ドライバーのみルーチンを呼び出し場合、miniclass ドライバーできます間での Win32 アプリケーションをサポートし、テープ miniclass インターフェイスを使用するテープ クラス ドライバーを提供するマイクロソフト オペレーティング システムに移植できます。 テープの miniclass ドライバーには、ヘッダー ファイルが含まれています。 *minitape.h*します。

既存のテープ miniclass ドライバーは、1 つ新しい入口を作成し、Windows 2000 と以降のオペレーティング システムで実行するために、TapeMiniGetMediaTypes をサポートするために変更する必要があります。 その他の変更は必要ありません。 システム提供のテープ クラス ドライバー、およびシステムが指定したストレージ ポート ドライバー、プラグ アンド プレイのハンドルとテープ miniclass ドライバーの代わりに電源管理要求。

このセクションでは、オペレーティング システムに固有のテープのクラス ドライバーによって提供されるサポートについて説明し、新しいテープ miniclass ドライバーを記述するためのガイドラインを提供します。 参照してください[テープ クラス ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[テープ Miniclass ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)のテープのルーチンの詳細については、クラスし、テープの miniclass ドライバー。 参照してください[デバイスの構成とドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-configurations-and-layered-drivers)ストレージ デバイス ドライバーのレイヤーの説明についてはします。

 

 




