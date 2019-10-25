---
title: マクロブロック制御コマンド構造の 4 番目の部分
description: マクロブロック制御コマンド構造の 4 番目の部分
ms.assetid: 26540693-09a2-4664-b0ac-4cc69e909e99
keywords:
- マクロは WDK DirectX VA、汎用コマンド構造をブロックします
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b08ae2dc476647052485a26591775df3a680a4b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838941"
---
# <a name="fourth-part-of-macroblock-control-command-structure"></a>マクロブロック制御コマンド構造の 4 番目の部分


## <span id="ddk_fourth_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FOURTH_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)の**b**の RPS メンバーと**bmv\_RPS**メンバーがゼロの場合、マクロブロックコントロールのコマンド構造は、「[マクロブロックコントロールのコマンド構造」の3番目の部分](third-part-of-macroblock-control-command-structure.md)で説明されているデータで終了します。 マクロブロックコントロールのコマンド構造は、必要に応じて、ゼロ値データが埋め込まれた構造体の3番目の部分で終了し、次のマクロブロックコントロールコマンドを16バイト境界に揃えます。

DXVA\_ピクチャパラメーターの**bDXVA** in メンバーがゼロで、\_ピクチャパラメーターの**BMV\_RPS**メンバーが1の場合、マクロブロックコントロールの4番目の部分は、という*バイトの配列になります。Bref絵文字 Select*。 配列内の要素の数は、前の表に示した**Mvector**配列内の要素の数と同じです。 配列の各要素は、 **Mvector**配列で見つかった対応するモーションベクターに関連付けられている非圧縮サーフェスのインデックスを指定します。 次に、マクロブロックコントロールのコマンド構造が終了し、必要に応じて、次のマクロブロックコントロールのコマンド構造を16バイトの境界に合わせるために、0値のデータが埋め込まれます。

 

 





