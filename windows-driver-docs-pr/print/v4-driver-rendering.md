---
title: V4 プリンター ドライバー レンダリング
description: V4 印刷ドライバー モデルを印刷デバイス用のページ記述言語に印刷ジョブを表示するためには、XPSDrv レンダリング モジュールを使用しています。
ms.assetid: 8952063C-3706-43A0-BA6B-231E7CD01514
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa8369d625a1c5e0ce9633243507b984a819c4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358674"
---
# <a name="v4-printer-driver-rendering"></a>V4 プリンター ドライバー レンダリング


V4 印刷ドライバー モデルの使用を印刷デバイス用のページ記述言語に印刷ジョブを表示するため、 [XPSDrv レンダリング モジュール](xpsdrv-render-module.md)します。

V4 ドライバー モデルは、他の目的、XPSDrv レンダー モジュールを使用しません。 ように XPS ダイレクト デバイス用のドライバーは、すべてのフィルターを含めるにはありません。 その他のすべてのデバイス ドライバーは、デバイスの PDL にレンダリングするフィルターを含める必要がありますか、またはを使用して印刷クラス ドライバーからの既存のレンダリング サポートを利用する必要があることが、 **RequiredClass** v4 のマニフェスト ファイルでディレクティブ。

ここでは、詳細については、v4 ドライバーのレンダリングで、次のトピックを示します。

[V4 プリンター ドライバーのレンダリング アーキテクチャ](v4-driver-rendering-architecture.md)

[XPSDrv の機能強化](improvements-in-xpsdrv.md)

[標準的な XPS のフィルター](standard-xps-filters.md)

[V4 印刷クラス ドライバーの表示](print-class-driver-rendering.md)

## <a name="related-topics"></a>関連トピック
[サポートされている PrintTicket 機能](supported-printticket-features.md)  
[V4 プリンター ドライバー](v4-printer-driver.md)  
[XPSDrv レンダー モジュール](xpsdrv-render-module.md)  



