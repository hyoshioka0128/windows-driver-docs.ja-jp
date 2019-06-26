---
title: ミニドライバー バージョン 5.07 の機能
description: ミニドライバー バージョン 5.07 の機能
ms.assetid: BFB38805-D2D3-40D2-B336-127B3B84141D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4973e8d5eae1f785fd5264a6adf847b9be2f3435
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356692"
---
# <a name="minidriver-version-507-features"></a>ミニドライバー バージョン 5.07 の機能


このバージョンでは、次の機能が導入されました。

## <a name="span-idchangestothecarddatastructurespanspan-idchangestothecarddatastructurespanspan-idchangestothecarddatastructurespanchanges-to-the-carddata-structure"></a><span id="Changes_to_the_CARD_DATA_structure"></span><span id="changes_to_the_card_data_structure"></span><span id="CHANGES_TO_THE_CARD_DATA_STRUCTURE"></span>カードに変更\_データ構造体


[**カード\_データ**](https://docs.microsoft.com/previous-versions/dn468748(v=vs.85))変更は、次を含む構造体します。

-   **DwVersion**メンバーとして、入力として扱われます、必要なバージョンから返される、 [ **CardAcquireContext** ](https://docs.microsoft.com/previous-versions/dn468701(v=vs.85))関数。 古いカードのミニドライバーはバージョン 4 のエントリのみをサポート可能性がありますが、ポイントします。 すべてのカードのミニドライバーは設定、返されるバージョンは&lt;= 渡されたバージョン。 この動作を既存の CSP からベース - と SC KSP ベースのカードのミニドライバーが更新されます。
-   **PfnCardPrivateKeyDecrypt**がメンバーに置き換え、 **pfnCardRSADecrypt**メンバー。 関連付けられている構造体と関数の型は、これを反映するように変更されました。
-   **PfnCardSign**メンバーを追加します。 これが埋め込まれていない入力のみを受け取るし、指定されたキーに基づく暗号署名を実行します。 ECC カードのミニドライバーの ECDSA 操作になります。
-   **PfnCardConstructDHAgreement**メンバーを追加します。 これは、1 つ Helman キーの承諾を実行します。 ECC カードのミニドライバーの ECDHE 操作になります。
-   **PfnCspPadData**エントリ ポイントを追加すると、カードのカードに埋め込みをサポートしていないことができますが、データが埋め込まれて CSP または KSP をコールバックできるようにします。

## <a name="span-idexpandedmeaningofthedwkeyspecparameterspanspan-idexpandedmeaningofthedwkeyspecparameterspanspan-idexpandedmeaningofthedwkeyspecparameterspanexpanded-meaning-of-the-dwkeyspec-parameter"></a><span id="Expanded_meaning_of_the_dwKeySpec_parameter"></span><span id="expanded_meaning_of_the_dwkeyspec_parameter"></span><span id="EXPANDED_MEANING_OF_THE_DWKEYSPEC_PARAMETER"></span>DwKeySpec パラメーターの意味を展開します。


意味、 **dwKeySpec**メンバーまたはパラメーター (さまざまな構造およびエントリ ポイントに存在) を展開します。

-   \_KEYEXCHANGE と AT\_署名が RSA キーとその使用目的を示します。 RSA キーのサイズでは、通常の流れに従います。
-   ECC キーは、サイズが非常に少なくなるし、正規の流れに従っていません。 ECC **dwKeySpec** AT などの正確なサイズを示す\_ECDHA\_P521 ECDHA の P 曲線 521 ビットのキー。 参照してください[ **CardCreateContainer** ](https://docs.microsoft.com/previous-versions/dn468708(v=vs.85))の新しい完全な一覧については**dwKeySpec**定数。

## <a name="span-idmanifestregistrationspanspan-idmanifestregistrationspanspan-idmanifestregistrationspanmanifest-registration"></a><span id="Manifest_registration"></span><span id="manifest_registration"></span><span id="MANIFEST_REGISTRATION"></span>マニフェストの登録


認識されているカード ATRs の登録はではなく、マニフェストを介して処理されようになりました*DllRegisterServer*と*DllUnRegisterServer*します。

## <a name="span-idinterfacesforsecretagreementchangesspanspan-idinterfacesforsecretagreementchangesspanspan-idinterfacesforsecretagreementchangesspaninterfaces-for-secret-agreement-changes"></a><span id="Interfaces_for_Secret_Agreement_Changes"></span><span id="interfaces_for_secret_agreement_changes"></span><span id="INTERFACES_FOR_SECRET_AGREEMENT_CHANGES"></span>インターフェイスの秘密協定の変更


ECDH シークレット契約変更用のインターフェイスが更新されます。

 

 





