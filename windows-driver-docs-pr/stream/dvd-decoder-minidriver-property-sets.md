---
title: DVD デコーダー ミニドライバーのプロパティ セット
description: DVD デコーダー ミニドライバーのプロパティ セット
ms.assetid: c24685bd-ea20-4cc2-b419-feb1fa2ea03e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 882c4fd988344d669d82f3338a19f81c10a801a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843219"
---
# <a name="dvd-decoder-minidriver-property-sets"></a>DVD デコーダー ミニドライバーのプロパティ セット


## <span id="ddk_dvd_decoder_minidriver_property_sets_ks"></span><span id="DDK_DVD_DECODER_MINIDRIVER_PROPERTY_SETS_KS"></span>


このセクションでは、Microsoft Windows 98/Me、Windows 2000、および Windows XP 以降で WDM カーネルストリーミングサービスを使用する DVD デコーダーミニドライバーで使用できる DVD デコーダー固有のプロパティセットについて説明します。

各プロパティの参照ページには、次に示す列見出しを持つテーブルが含まれています。


| [購入] | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

これらの見出しの意味は次のとおりです。

-   **取得**

    ターゲットの KS オブジェクトは、プロパティの取得\_\_型の KSK プロパティをサポートしていますか?

-   **一連**

    ターゲットの KS オブジェクトでは、プロパティ\_型\_SET プロパティがサポートされているかどうかを確認できます。

-   **接続**

    これは、プロパティ要求が送信される KS オブジェクトです。 DVD デコーダープロパティのターゲットは、フィルターまたは pin です。 (プロパティ要求では、カーネルハンドルによってターゲットオブジェクトが指定されます)。

-   **プロパティ記述子の型**

    プロパティ記述子は、プロパティと、そのプロパティに対して実行する操作を指定します。 記述子は常に[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)構造で始まります。

-   **プロパティ値の型**

    プロパティには値があり、この値の型はプロパティによって異なります。 たとえば、の2つの状態 (オンまたはオフ) のいずれかであるプロパティは、通常、ブール値を持ちます。 0から0xFFFFFFFF の整数値を想定できるプロパティは、ULONG 値を持つ場合があります。 より複雑なプロパティには、配列または構造体の値が含まれる場合があります。

上記のプロパティ記述子とプロパティ値は、 [「KS プロパティ、イベント、およびメソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)」で説明されている、インスタンス仕様および操作データバッファーのプロパティ固有バージョンです。

プロパティ要求では、次のいずれかのフラグを使用して、プロパティに対して実行する操作を指定します。

-   KSPROPERTY\_TYPE\_BASICSUPPORT

-   KSK プロパティ\_TYPE\_GET

-   KSK プロパティ\_TYPE\_SET

すべてのフィルターオブジェクトとピンオブジェクトは、そのプロパティに対する基本サポート操作をサポートしています。 *Get*操作と*Set*操作をサポートするかどうかは、プロパティによって異なります。 Filter オブジェクトまたは pin オブジェクトの固有の機能を表すプロパティは、get 操作のみを必要とする可能性があります。 構成可能な設定を表すプロパティは、設定操作のみを必要とする場合がありますが、get 操作は現在の設定の読み取りにも便利な場合があります。 DVD デコーダーのプロパティで get、set、および basic サポート操作を使用する方法の詳細については、「 [KS のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)」を参照してください。

プロパティは、ストリームの側面を照会または変更します。 いくつかのプロパティセットが DVD デコーダーに使用されます。 すべての DVD デコーダー入力ストリームは、このトピックで説明するプロパティセットに加えて、DVD の著作権保護のプロパティセットをサポートします。

すべてのプロパティの説明には、プロパティの読み取りまたは書き込みをサポートするために DVD デコーダーミニドライバーが必要かどうかを示す表が含まれています。 DVD デコーダーミニドライバーは、ミニドライバーでサポートされていないプロパティの取得または設定要求に対して\_サポートされていない状態\_返す必要があります。

次のプロパティセットは、DVD デコーダーミニドライバーに対して定義されています。

[KSPROPSETID\_AudioDecoderOut](kspropsetid-audiodecoderout.md)

[KSPROPSETID\_DvdSubPic](kspropsetid-dvdsubpic.md)

[KSPROPSETID\_CopyProt](kspropsetid-copyprot.md)

[KSPROPSETID\_TSRateChange](kspropsetid-tsratechange.md)

[KSPROPSETID\_VPConfig および KSPROPSETID\_VPVBIConfig](kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig.md)

[KSPROPSETID\_Wave](kspropsetid-wave.md)

 

 





