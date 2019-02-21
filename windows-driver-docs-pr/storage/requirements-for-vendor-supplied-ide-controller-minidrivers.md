---
title: ベンダーから提供された IDE コント ローラーのミニドライバーの要件
description: ベンダーから提供された IDE コント ローラーのミニドライバーの要件
ms.assetid: a1584665-8788-49a4-b86f-50c265e7ce7a
keywords:
- ベンダーから提供された、IDE コント ローラー ミニドライバー WDK ストレージ
- 記憶域 IDE コント ローラー ミニドライバー WDK、ベンダーから提供されました。
- IDE コント ローラーのミニドライバー WDK ストレージをベンダーから提供されました。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c6db1bc511f5dc21e4d8e6c3ccd7ef3a1c3a568
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529142"
---
# <a name="requirements-for-vendor-supplied-ide-controller-minidrivers"></a>ベンダーから提供された IDE コント ローラーのミニドライバーの要件


## <span id="ddk_requirements_for_vendor_supplied_ide_controller_minidrivers_kg"></span><span id="DDK_REQUIREMENTS_FOR_VENDOR_SUPPLIED_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


このセクションでは、IDE コント ローラーのミニドライバーのベンダーから提供された Microsoft Windows の要件について説明します。

Microsoft 提供の IDE ポート ドライバー *atapi.sys*とコント ローラー ドライバーが*pciidex.sys*ハードウェアに依存しないし、ほぼすべての IDE コント ローラーで使用できます。 そのため、ベンダーから提供されたポートおよびコント ローラーのドライバーは必要ありません。

Microsoft は、ネイティブのコント ローラー ミニドライバーも提供*問題は、pciide.sys*、コント ローラー ドライバー ミニドライバーのペアのハードウェア依存の側面を処理して、ほとんどの IDE コント ローラーのハードウェアで使用できます。 使用する代わりに、独自のコント ローラー ミニドライバーを指定することを選択できますベンダー*問題は、pciide.sys*します。

コント ローラーのベンダーから提供されたミニドライバーは、プラグ アンド プレイ (PnP) または電源の管理をサポートする必要はありません。 PnP ドライバー パッケージと電源管理操作は、Microsoft 提供のコント ローラー ドライバーによって処理されます*pciidex.sys*します。

コント ローラーのベンダーから提供されたミニドライバーは、システムの要件に準拠する、特定のインターフェイスを登録する必要はありません。

コント ローラーのベンダーから提供されたミニドライバーは、レジストリにアクセスしようとはしないでください。 また PciIdeX ライブラリによって提供されるもの以外のカーネル モードのルーチンを呼び出すことが必要があります。

コント ローラーのベンダーから提供されたミニドライバーは、ハードウェアに依存する操作を透過的に実行するシステム提供のコント ローラー ドライバーが使用できる標準のミニドライバー ルーチンのセットを提供する必要があります。

PciIdeX ライブラリと、コント ローラーのシステム提供のドライバーとコント ローラーのベンダーから提供されたミニドライバーのミニドライバーの日常的なインターフェイスの説明の詳細については、次を参照してください[初期化し、IDE のミニドライバーの呼び出し。ルーチン](initializing-and-calling-ide-minidriver-routines.md)します。

 

 




