---
title: FVF コードの変更
description: FVF コードの変更
ms.assetid: d9db4356-570b-4e05-aec9-bf36e26e4570
keywords:
- FVF WDK Direct3D
- 複数の行列による頂点のブレンド WDK Direct3D、FVF コードの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e0a5cafe4915d6e2b67a3234e1054cabc2b7ee7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527839"
---
# <a name="fvf-code-changes"></a>FVF コードの変更


## <span id="ddk_fvf_code_changes_gg"></span><span id="DDK_FVF_CODE_CHANGES_GG"></span>


複数の行列による頂点のブレンド キー API への影響は、柔軟な頂点の書式 (FVF) の位置コンポーネントに重みパラメーターをブレンドする頂点を追加します。 これらのパラメーターは、32 ビット IEEE 単精度浮動小数点数として格納されます。 FVF コードの 4 つの新しいビット パターンの追加により入力頂点データに存在すると、表されます。D3DVFV\_XYZB2、D3DVFV\_XYZB3、D3DVFV\_XYZB4、および D3DVFV\_XYZB5 します。

これらのコードでは、余分な Dword またはパーティクル丸める半径などの他の使用に割り当て可能な領域または霧パラメーターに応じて、機能は有効になっているを特定します。

**注**  場合 blend の重みを指定の数は 1 つの行列のブレンド現在されて、最後のマトリックスに割り当てられた重みとして定義されているし、(1.0 - Bₜ) Bₜ がその頂点の他の重みの合計を数よりも小さい.

 

 

 





