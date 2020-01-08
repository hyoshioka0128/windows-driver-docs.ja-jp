---
title: ベンダー提供の IDE コントローラーミニドライバーの概要
description: ベンダー提供の IDE コントローラー ミニドライバーの要件
ms.assetid: a1584665-8788-49a4-b86f-50c265e7ce7a
keywords:
- IDE コントローラーミニドライバー WDK storage、ベンダ提供
- ストレージ IDE コントローラーミニドライバー WDK、ベンダ提供
- ベンダーが提供する IDE コントローラーミニドライバー WDK ストレージ
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: d094bb79b40e2aaf2f93438ae0ae251e77466300
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606560"
---
# <a name="introduction-to-vendor-supplied-ide-controller-minidrivers"></a>ベンダー提供の IDE コントローラーミニドライバーの概要

Microsoft が提供する IDE ポートドライバー、 *atapi*、およびコントローラードライバー *pciidex*はハードウェアに依存しないため、ほとんどすべての ide コントローラーで使用できます。 したがって、ベンダーから提供されたポートドライバーとコントローラードライバーは必要ありません。

また、Microsoft では、ミニドライバーというネイティブコントローラーを提供して*います。 pciide*は、コントローラードライバーミニドライバーペアのハードウェアに依存する側面を処理し、ほとんどの IDE コントローラーハードウェアで使用できます。 ベンダーは、 *pciide*を使用する代わりに、独自のコントローラーミニドライバーを指定することができます。

ベンダーから提供されたコントローラーミニドライバー:

- では、プラグアンドプレイ (PnP) または電源管理をサポートする必要はありません。 PnP および電源管理操作は、Microsoft が提供するコントローラードライバーである*pciidex*によって処理されます。

- システム要件に準拠するために、特定のインターフェイスを登録する必要はありません。

- レジストリにアクセスしたり、 *PciIdeX*ライブラリによって提供されるもの以外のカーネルモードルーチンを呼び出したりすることはできません。

- では、システムによって提供されるコントローラードライバーがハードウェアに依存する操作を透過的に行うことを許可する一連の標準ミニドライバールーチンを提供する必要があります。

*PciIdeX*ライブラリの詳細と、システムによって提供されるコントローラードライバーとベンダーが提供するコントローラーミニドライバー間のミニドライバールーチンインターフェイスの説明については、「 [IDE ミニドライバールーチンの初期化と呼び出し](initializing-and-calling-ide-minidriver-routines.md)」を参照してください。

 

 




