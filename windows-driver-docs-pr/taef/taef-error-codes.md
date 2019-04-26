---
title: TAEF のエラー コード
description: TAEF のエラー コード
ms.assetid: E42AF880-12DA-42b7-AB6D-90011BD7E548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a2a34a048178dea5ef2bddd692b1094acca3a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347996"
---
# <a name="taef-error-codes"></a>TAEF のエラー コード


TAEF には、クロス マシン実行またはテストのよく知られているメタデータの無効な値を受け取るのために、マシンに接続できませんかの理由であるなどのさまざまなエラーが発生することができます。 エラーが発生すると、TAEF は多くの場合のエラー メッセージとエラーに関連付けられている HRESULT 値を示しています。 HRESULT 値のほとんどは[既知のシステム エラー コード](https://msdn.microsoft.com/library/ms681381.aspx)TAEF はカスタム エラー コードを示すことがありますが、します。

## <a name="span-idcustomtaefhresultvaluesspanspan-idcustomtaefhresultvaluesspanspan-idcustomtaefhresultvaluesspancustom-taef-hresult-values"></a><span id="Custom_TAEF_HRESULT_Values"></span><span id="custom_taef_hresult_values"></span><span id="CUSTOM_TAEF_HRESULT_VALUES"></span>カスタム TAEF HRESULT 値


TAEF のカスタムの HRESULT 値は、追加された次の表に記載されます。 現時点では、1 つだけの TAEF 特有の HRESULT 値があります。

| HRESULT                             | 値      | 説明                                                                                                                                                                                                                                    |
|-------------------------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TAEF\_E\_無効な\_テスト\_環境 | 0x81A40001 | TAEF テストでは、そのメタデータを使用して無効なテスト環境を要求します。 テスト環境に影響するメタデータの例を示します[RunAs](runas.md)、 [ThreadingModel](threading-models.md)、および[ActivationContext](activation-context.md)します。 |

 

 

 





