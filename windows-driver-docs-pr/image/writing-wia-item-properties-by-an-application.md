---
title: アプリケーションによる WIA 項目のプロパティの書き込み
description: アプリケーションによる WIA 項目のプロパティの書き込み
ms.assetid: 728f3f73-4815-4d79-ac02-227de7ae9bb7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4986a4f06aab19a1e4eb5adfd03c19ec46d078d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365002"
---
# <a name="writing-wia-item-properties-by-an-application"></a>アプリケーションによる WIA 項目のプロパティの書き込み





WIA アプリケーション WIA プロパティに書き込みます (と更新プログラムのプロパティに格納されている値)、WIA サービスにより、WIA ミニドライバーを呼び出すことで受信した値を検証する営業案件、 [ **IWiaMiniDrv:。drvValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)メソッド。 WIA ミニドライバーは、ドライバー項目ツリー内のプロパティを読み取ることによって、現在の値に、受信した値を比較します。 WIA サービス ライブラリでは、これらの値にアクセスするための機能を提供します。

**IWiaMiniDrv::drvValidateItemProperties**メソッドは、次のタスクを実行する必要があります。

1.  項目の種類を決定します。

2.  着信 WIA プロパティのいずれかの特別な検証を実行する必要があるかどうかを決定します。 WIA プロパティが書き込まれているためには、WIA ミニドライバーは、(PROPSPEC 構造体は、Microsoft Windows SDK ドキュメントで説明) PROPSPEC 構造体の配列を使用できます。 配列を走査する必要性の軽減 PROPSPEC 配列を処理する前に、WIA ミニドライバーが項目の種類を調べることをお勧めすべて**IWiaMiniDrv::drvValidateItemProperties**呼び出します。 特別な検証の要件が存在しないか、唯一の書き込みの要求が子項目のプロパティ、デバイスのルート項目に依存するプロパティを更新する必要がある場合がある場合は処理されます。

3.  WIA 項目の依存プロパティを更新する必要があります WIA プロパティの検証中に変更された値にアクセスする WIA プロパティ コンテキストを作成します。 使用して、 [ **wiasCreatePropContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)と **wiasGetChangedValue * * * Xxx*サービスの機能です。

4.  WIA サービス関数を使用して、依存プロパティを更新[ **wiasWriteMultiple** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)または **wiasWriteProp * * * Xxx*、可能性がありますが、有効な値の更新が含まれますプロパティの設定の結果が変更されました。 など、WIA ミニドライバーは、設定をサポートしている場合、 [ **WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)プロパティ、アプリケーション、の変更時に有効なビット深度のリストを更新する必要があります[**WIA\_IPA\_DATATYPE** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)プロパティ。

    ときの値、 [ **WIA\_IPA\_DATATYPE** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype) WIA からプロパティの変更\_データ\_WIA をしきい値\_データ\_色、関連する WIA\_IPA\_24 ビットまたは 48 ビットのレポートに 1 ビット色をレポートから DEPTH プロパティを変更します。

5.  呼び出す、 [ **wiasValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties) WIA サービスを他のすべてのプロパティの要求を検証する関数のサービスを提供します。 これは、「キャッチ オール」のケースでは、します。WIA サービスでは、組み込みのプロパティの検証があります。

 

 




