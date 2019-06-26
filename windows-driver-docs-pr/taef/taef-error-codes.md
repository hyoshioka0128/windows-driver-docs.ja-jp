---
title: TAEF のエラー コード
description: TAEF のエラー コード
ms.assetid: E42AF880-12DA-42b7-AB6D-90011BD7E548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 553725b100ead4251ac9bcd96dd84a5cf028069e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372994"
---
# <a name="taef-error-codes"></a>TAEF のエラー コード


TAEF には、クロス マシン実行またはテストのよく知られているメタデータの無効な値を受け取るのために、マシンに接続できませんかの理由であるなどのさまざまなエラーが発生することができます。 エラーが発生すると、TAEF は多くの場合のエラー メッセージとエラーに関連付けられている HRESULT 値を示しています。 HRESULT 値のほとんどは[既知のシステム エラー コード](https://docs.microsoft.com/windows/desktop/Debug/system-error-codes)TAEF はカスタム エラー コードを示すことがありますが、します。

## <a name="span-idcustomtaefhresultvaluesspanspan-idcustomtaefhresultvaluesspanspan-idcustomtaefhresultvaluesspancustom-taef-hresult-values"></a><span id="Custom_TAEF_HRESULT_Values"></span><span id="custom_taef_hresult_values"></span><span id="CUSTOM_TAEF_HRESULT_VALUES"></span>カスタム TAEF HRESULT 値


TAEF のカスタムの HRESULT 値は、追加された次の表に記載されます。 現時点では、1 つだけの TAEF 特有の HRESULT 値があります。

| HRESULT                             | Value      | 説明                                                                                                                                                                                                                                    |
|-------------------------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TAEF\_E\_無効な\_テスト\_環境 | 0x81A40001 | TAEF テストでは、そのメタデータを使用して無効なテスト環境を要求します。 テスト環境に影響するメタデータの例を示します[RunAs](runas.md)、 [ThreadingModel](threading-models.md)、および[ActivationContext](activation-context.md)します。 |

 

 

 





