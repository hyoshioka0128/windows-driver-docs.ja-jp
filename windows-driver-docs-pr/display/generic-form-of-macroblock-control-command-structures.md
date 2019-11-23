---
title: マクロブロック制御コマンド構造の一般的なフォーム
description: マクロブロック制御コマンド構造の一般的なフォーム
ms.assetid: 44009238-0a8e-4018-9b50-06729640f5e4
keywords:
- マクロは WDK DirectX VA、汎用コマンド構造をブロックします
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3249f98367e8a402e85aec76d7c571c28152af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839675"
---
# <a name="generic-form-of-macroblock-control-command-structures"></a>マクロブロック制御コマンド構造の一般的なフォーム


## <span id="ddk_generic_form_of_macroblock_control_command_structures_gg"></span><span id="DDK_GENERIC_FORM_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURES_GG"></span>


*Dxva*で明示的に定義されている次のマクロブロックコントロール構造は、DirectX VA でマクロブロックコントロールコマンドに使用される一般的なデザインの特殊なケースです。

[**DXVA\_MBctrl\_I\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)

[**DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)

[**DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)

これらの構造体は、最も一般的に使用されるマクロブロックコントロールコマンドのみを表します。 これらの既存の構造の設計に基づいて、他のマクロブロックコントロールコマンドを作成して、ドライバーが他のビデオデコード要素をサポートし、デコードプロセスのさまざまな構成を処理できるようにすることができます。

このセクションでは、マクロブロックコントロールの追加コマンドを作成するための基礎として使用される汎用マクロブロックコントロールコマンドの構造体のメンバーについて説明します。 このセクションのマクロブロックコントロールコマンドの構造体の定義は、4つの部分に分かれています。

**注**   マクロブロックコントロールコマンドは、16バイトのメモリ境界に配置され、1バイトの配置パッキングを使用するパックされたデータ構造として構築されます。

 

 

 





