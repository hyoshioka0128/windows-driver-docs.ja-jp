---
title: コマンドのマクロ ブロックの制御構造の一般的なフォーム
description: コマンドのマクロ ブロックの制御構造の一般的なフォーム
ms.assetid: 44009238-0a8e-4018-9b50-06729640f5e4
keywords:
- マクロ ブロック WDK DirectX va なので、汎用的なコマンド構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cb8d6a9bd201341c4d06c19ebdbf2ae65fc3af6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539211"
---
# <a name="generic-form-of-macroblock-control-command-structures"></a>コマンドのマクロ ブロックの制御構造の一般的なフォーム


## <span id="ddk_generic_form_of_macroblock_control_command_structures_gg"></span><span id="DDK_GENERIC_FORM_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURES_GG"></span>


次のマクロ ブロック制御構造がで明示的に定義*dxva.h* DirectX VA のマクロ ブロック コントロール コマンドに使用する汎用的な設計の特殊なケースします。

[**DXVA\_MBctrl\_I\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563983)

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563989)

[**DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)

[**DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563997)

これらの構造は、最もよく使用されるマクロ ブロック コントロール コマンドの形式のみを表します。 その他のビデオのデコード要素をサポートし、デコード処理ごとに異なる構成を処理するために、ドライバーを許可するこれらの既存の構造の設計に基づいて、マクロ ブロックの追加コントロールのコマンドを作成できます。

このセクションでは、追加マクロ ブロックに制御コマンドを作成するための基礎として使用されるジェネリックのマクロ ブロック コントロール コマンド構造体のメンバーについて説明します。 このセクションではマクロ ブロック コントロール コマンドの構造体の定義は、4 つの部分に分かれています。

**注**  マクロ ブロック コントロール コマンドが 16 バイトのメモリ境界に揃えて配置と 1 バイト アラインメントの梱包にパックされたデータ構造体として構築します。

 

 

 





