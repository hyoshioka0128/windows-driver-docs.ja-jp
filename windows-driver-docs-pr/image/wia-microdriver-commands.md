---
title: WIA Microdriver コマンド
description: WIA Microdriver コマンド
ms.assetid: 54d0c35b-d8b3-4e38-85cf-d5b4f80f6daa
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9d7f58639a5025b1b0b91076a02884d5dac1d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536521"
---
# <a name="wia-microdriver-commands"></a>WIA Microdriver コマンド


## <span id="ddk_wia_microdriver_commands_si"></span><span id="DDK_WIA_MICRODRIVER_COMMANDS_SI"></span>


次のセットします定数フォーム WIA microdriver コマンドのセット。 コマンドは、WIA ベッド ドライバーから、microdriver に渡される、 *lCommand*のパラメーター、 [ **MicroEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff545248)関数。 コマンドは、次のカテゴリに分類されます。

-   [自動ドキュメント フィーダー コマンド](automatic-document-feeder-commands.md)

    Microdrivers 自動ドキュメント フィーダー (ADF) をサポートするためのコマンド。

-   [イベント コマンド](event-commands.md)

    Microdriver イベント サポート用のコマンド。

-   [必要なコマンド](required-commands.md)

    Microdriver によって実装する必要がありますコマンド。

-   [省略可能なコマンド](optional-commands.md)

    その基本的な操作の機能強化として、microdriver によって実装できるコマンド。

これらのコマンドが定義されている*Wiamicro.h*は、Windows XP と Windows Me で使用できる以降とします。

 

 





