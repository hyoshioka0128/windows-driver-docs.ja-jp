---
title: 拡張 Blt フラグ
description: 拡張 Blt フラグ
ms.assetid: 9c2f7013-dd58-4a61-b452-d263f5caf0d0
keywords:
- 拡張 blt WDK DirectX 9.0 をフラグします。
- DDBLT_EXTENDED_FLAGS
- blt フラグの拡張機能 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c19ba45ea4eee42f5220540a5ea04d337c8d6e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530851"
---
# <a name="extended-blt-flags"></a>拡張 Blt フラグ


## <span id="ddk_extended_blt_flags_gg"></span><span id="DDK_EXTENDED_BLT_FLAGS_GG"></span>


DirectX 9.0 の使用、DDBLT\_拡張\_DDBLT の使用を拡張する blt フラグをフラグ\_*Xxx* blt フラグで利用できる、 **dwFlags** のメンバー[ **DD\_BLTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550474)構造体。 DirectX 9.0 ランタイムが、ディスプレイ ドライバーを呼び出すときに[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205) blt 操作を実行する関数をランタイムは DDBLT を組み合わせることができます\_拡張\_DDBLTフラグ\_*Xxx*フラグのビットごとの OR を使用して、フラグの新しい意味を作成します。 ドライバー DDBLT のプレゼンスを決定し\_拡張\_フラグ、フラグのビットとして再解釈し、それに応じて blt 操作を実行します。 ドライバーはかどうかを決定する場合は、このメカニズムを使用して[ガンマ補正を実行](performing-gamma-correction-on-swap-chains.md)をデスクトップにバック バッファーから blt 中に線形のカラー スペース上。 ドライバーは、どうかを判断拡張 blt フラグを使用することも[stretch blit 操作](supporting-stretch-blit-operations.md)要求されます。

 

 





