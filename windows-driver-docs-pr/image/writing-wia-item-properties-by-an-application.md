---
title: アプリケーションによる WIA 項目のプロパティの書き込み
description: アプリケーションによる WIA 項目のプロパティの書き込み
ms.assetid: 728f3f73-4815-4d79-ac02-227de7ae9bb7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad6910d4ad692fe9ed8dd6b92c804a95a159bb11
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840660"
---
# <a name="writing-wia-item-properties-by-an-application"></a>アプリケーションによる WIA 項目のプロパティの書き込み





Wia アプリケーションが WIA プロパティに書き込み、プロパティに格納されている値を更新すると、wia サービスは[**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)メソッドを呼び出すことにより、受信した値を検証する機会を wia ミニドライバーに与えます。 WIA ミニドライバーは、独自のドライバー項目ツリーのプロパティを読み取って、受信した値と現在の値を比較します。 WIA サービスライブラリには、これらの値にアクセスするための関数が用意されています。

**IWiaMiniDrv::D rvvalidateitemproperties**メソッドでは、次のタスクを実行する必要があります。

1.  項目の種類を決定します。

2.  受信した WIA プロパティで特別な検証を実行する必要があるかどうかを判断します。 どの WIA プロパティが書き込まれているかを判断するために、WIA ミニドライバーは PROPSPEC 構造の配列を使用できます (PROPSPEC 構造については Microsoft Windows SDK のドキュメントを参照してください)。 **IWiaMiniDrv::D rvvalidateitemproperties**の呼び出しのたびに配列を走査する必要性を減らすために、propspec 配列を処理する前に、WIA ミニドライバーが項目の種類を決定することをお勧めします。 特別な検証要件がない場合、またはデバイスのルート項目の依存プロパティを更新する必要がある場合は、子項目のプロパティに対する書き込み要求のみが処理されます。

3.  Wia プロパティコンテキストを作成して、wia プロパティの検証中に変更された値にアクセスします。これは、WIA 項目の依存プロパティを更新するために必要です。 [**Wiascreatepropcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)および **Wiasget値 * * * Xxx*サービス関数を使用します。

4.  WIA サービス関数[**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)または **Wiaswriteprop * * * Xxx*を使用して、依存プロパティを更新します。これには、プロパティを設定した結果として変更された可能性のある有効な値の更新が含まれます。 たとえば、wia ミニドライバーで wia [ **\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)プロパティの設定がサポートされている場合は、アプリケーションが[**wia\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)プロパティを変更したときに、ビット深度の有効な一覧を更新する必要があります。

    Wia [ **\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)プロパティの値が WIA\_DATA\_THRESHOLD から WIA\_データ\_の色に変更された場合、関連する WIA\_IPA\_DEPTH プロパティは、レポートの1ビットカラーに変更されます。詳細。24ビットまたは48ビットを報告します。

5.  [**WiasValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties) service 関数を呼び出して、他のすべてのプロパティ要求を WIA サービスで検証できるようにします。 これは "キャッチオール" ケースです。WIA サービスには、組み込みのプロパティ検証があります。

 

 




