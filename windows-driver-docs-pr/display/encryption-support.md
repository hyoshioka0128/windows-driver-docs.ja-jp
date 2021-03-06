---
title: 暗号化のサポート
description: 暗号化のサポート
ms.assetid: d5ce9c02-7126-4775-bb87-dae45b93b652
keywords:
- ビデオのデコード WDK DirectX VA, 暗号化
- ビデオのデコードの WDK DirectX VA, 暗号化
- 画像のデコード WDK DirectX VA, 暗号化
- WDK DirectX VA の暗号化
- WDK DirectX VA の暗号化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfda7421910252e004d9ad46718e05bc77017d78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355561"
---
# <a name="encryption-support"></a>暗号化のサポート


## <span id="ddk_encryption_support_gg"></span><span id="DDK_ENCRYPTION_SUPPORT_GG"></span>


次の構造とデータの種類のビデオのデコードに使用するデータを暗号化できます。

-   マクロ ブロック制御コマンドの構造

-   ブロック構造の残存の違い

-   ビット ストリーム バッファー

ホストをデコーダーが暗号化を使用するためには、アクセラレータがどのような種類の暗号化をサポートそれを判断する必要があります。 アクセラレータでサポートされている暗号化の種類についての情報は、ビデオ アクセラレータ形式の Guid としてホストに提供される暗号化の種類の Guid のリストに含まれます。 ビデオ アクセラレータ形式の Guid の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**注**  すべての DirectX VA アクセラレータは、暗号化を使用せずに動作するようである必要があります。 暗号化、そのため、しなくても宣言することがなくを操作するためにサポートし、DXVA\_NoEncrypt「暗号化なし」GUID する必要がありますが送信されないビデオ アクセラレータ形式の GUID の一覧でします。

 

ホストは、適用する暗号化プロトコルの種類を選択し、アクセラレータに GUID を送信することによってこの選択肢を示します。 暗号化されたデータが正常に転送される前に、一般的な暗号化のシナリオでは、2 つ詳細について手順が実行です。

1.  ホスト デコーダーは、データを受信するアクセラレータが許可されている検証を必要があります。 アクセラレータの承認済みの公開/秘密キー ペアを保持していることを証明するために、ホストに署名された構造体を渡すことで、この検証を指定できます。

2.  次に、ホスト デコーダーはアクセラレータに暗号化されたコンテンツ キーを送信します。

暗号化プロトコルを初期化するための手順の正確な数は、使用されている暗号化の種類とその実装方法によって異なります。

必要な暗号化方式の初期化パラメーターを渡すには、ホストとアクセラレータ間で交換される各データ セットは、暗号化プロトコルの種類の GUID によってプレフィックス指定する必要があります。 この GUID は、別のデータからの暗号化の 1 つの種類のデータを区別します。 これは、機能は、暗号化の種類を 1 つは、1 つの DirectX VA バッファーの使用可能であり、別の DirectX VA バッファーの別の種類の暗号化を使用できますので必要です。

[ **DXVA\_EncryptProtocolHeader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_encryptprotocolheader)構造を使用して、暗号化プロトコルが使用されている暗号化の種類と使用されていることを示します。

 

 





