---
title: WIA マイクロドライバーのコマンド
description: WIA マイクロドライバーのコマンド
ms.assetid: 54d0c35b-d8b3-4e38-85cf-d5b4f80f6daa
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a64a3c23a3671ab8ded151c7d8f337a17ad2d6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840680"
---
# <a name="wia-microdriver-commands"></a>WIA マイクロドライバーのコマンド


## <span id="ddk_wia_microdriver_commands_si"></span><span id="DDK_WIA_MICRODRIVER_COMMANDS_SI"></span>


次の一連の定数は、一連の WIA マイクロドライバコマンドを形成します。 コマンドは、 [**Microdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-microentry)関数の*lcommand*パラメーターで、WIA フラットドライバーからマイクロドライバーに渡されます。 これらのコマンドは、次のカテゴリに分類されます。

-   [ドキュメントフィーダーの自動コマンド](automatic-document-feeder-commands.md)

    自動ドキュメントフィーダー (ADF) をサポートするマイクロドライバーのコマンド。

-   [イベントコマンド](event-commands.md)

    マイクロドライバイベントのサポート用コマンド。

-   [必須のコマンド](required-commands.md)

    マイクロドライバによって実装される必要があるコマンド。

-   [省略可能なコマンド](optional-commands.md)

    マイクロドライバによって基本操作の拡張として実装できるコマンド。

これらのコマンドは*Wiamicro. h*で定義されており、windows Me および windows XP 以降で使用できます。

 

 





