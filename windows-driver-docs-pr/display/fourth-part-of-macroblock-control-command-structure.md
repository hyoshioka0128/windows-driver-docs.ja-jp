---
title: マクロブロック制御コマンド構造の 4 番目の部分
description: マクロブロック制御コマンド構造の 4 番目の部分
ms.assetid: 26540693-09a2-4664-b0ac-4cc69e909e99
keywords:
- マクロ ブロック WDK DirectX va なので、汎用的なコマンド構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45dbd5742ebbddfd0d781f5953c18e81de2b941f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325346"
---
# <a name="fourth-part-of-macroblock-control-command-structure"></a>マクロブロック制御コマンド構造の 4 番目の部分


## <span id="ddk_fourth_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FOURTH_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


場合、 **bPicIntra**と**bMV\_RPS**のメンバー [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012) 0 の場合は、マクロ ブロック コントロール コマンド構造で説明されているデータで終わる[マクロ ブロック コントロール コマンド構造の 3 番目一部](third-part-of-macroblock-control-command-structure.md)します。 マクロ ブロック コントロール コマンド構造は、必要に応じて、16 バイト境界には、次のマクロ ブロック コントロール コマンドを配置する場合、データの値が 0 で埋められます構造体の第 3 部で終わっています。

場合、 **bPicIntra**の DXVA メンバー\_PictureParameters は 0、 **bMV\_RPS** DXVA のメンバー\_PictureParameters は 1、4 番目の部分、マクロ ブロック コントロール コマンドの構造と呼ばれるバイトの配列は、 *bRefPicSelect*します。 その配列内の要素の数は、要素の数と同じ、 **MVector**配列は、前の表に示すようにします。 配列の各要素に対応する動きベクトルに関連付けられている、圧縮されていない画面のインデックスを指定する、 **MVector**配列。 次のマクロ ブロックに制御コマンドの構造が終了しは、必要に応じて、16 バイト境界に次のマクロ ブロック コントロール コマンドの構造体を整列するデータの値が 0 で埋められます。

 

 





