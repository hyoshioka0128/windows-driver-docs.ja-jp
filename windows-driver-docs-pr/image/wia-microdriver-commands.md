---
title: WIA マイクロドライバーのコマンド
description: WIA マイクロドライバーのコマンド
ms.assetid: 54d0c35b-d8b3-4e38-85cf-d5b4f80f6daa
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 857678af1b7c9142d525718bfe851008dc5b6ac1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355199"
---
# <a name="wia-microdriver-commands"></a>WIA マイクロドライバーのコマンド


## <span id="ddk_wia_microdriver_commands_si"></span><span id="DDK_WIA_MICRODRIVER_COMMANDS_SI"></span>


次のセットします定数フォーム WIA microdriver コマンドのセット。 コマンドは、WIA ベッド ドライバーから、microdriver に渡される、 *lCommand*のパラメーター、 [ **MicroEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/nf-wiamicro-microentry)関数。 コマンドは、次のカテゴリに分類されます。

-   [自動ドキュメント フィーダー コマンド](automatic-document-feeder-commands.md)

    Microdrivers 自動ドキュメント フィーダー (ADF) をサポートするためのコマンド。

-   [イベント コマンド](event-commands.md)

    Microdriver イベント サポート用のコマンド。

-   [必要なコマンド](required-commands.md)

    Microdriver によって実装する必要がありますコマンド。

-   [省略可能なコマンド](optional-commands.md)

    その基本的な操作の機能強化として、microdriver によって実装できるコマンド。

これらのコマンドが定義されている*Wiamicro.h*は、Windows XP と Windows Me で使用できる以降とします。

 

 





