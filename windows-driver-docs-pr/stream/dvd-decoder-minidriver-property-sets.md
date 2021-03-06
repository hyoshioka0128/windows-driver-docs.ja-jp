---
title: DVD デコーダー ミニドライバーのプロパティ セット
description: DVD デコーダー ミニドライバーのプロパティ セット
ms.assetid: c24685bd-ea20-4cc2-b419-feb1fa2ea03e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0296cc1724e547ef9039ae925860a7663ae159c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358428"
---
# <a name="dvd-decoder-minidriver-property-sets"></a>DVD デコーダー ミニドライバーのプロパティ セット


## <span id="ddk_dvd_decoder_minidriver_property_sets_ks"></span><span id="DDK_DVD_DECODER_MINIDRIVER_PROPERTY_SETS_KS"></span>


このセクションには、Microsoft Windows 98 で WDM カーネル ストリーミング サービスを使用する DVD デコーダー ミニドライバーで利用可能な DVD デコーダーに固有のプロパティ セットがについて説明します/Me、Windows 2000 および Windows XP 以降。

各プロパティのリファレンス ページには、次のような列見出しのテーブルが含まれています。


| 取得 | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

これらの見出しには、次の意味があります。

-   **取得**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_プロパティの GET 要求ですか?

-   **設定**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_セット プロパティ要求でしょうか。

-   **移行先**

    これは、どのプロパティに要求が送信された KS オブジェクトです。 DVD デコーダー プロパティの対象は、フィルターまたは pin のいずれかです。 (プロパティ要求を指定します、ターゲット オブジェクトがカーネル ハンドルによって。)

-   **プロパティ記述子の型**

    プロパティ記述子には、プロパティとそのプロパティに対して実行する操作を指定します。 記述子は常に始まり、 [ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)構造体。

-   **プロパティ値の型**

    プロパティの値を持つし、この値の型は、プロパティによって異なります。 たとえば、オンまたはオフ----だけ 2 つの状態のいずれかの可能性のあるプロパティには、ブール値を通常があります。 ULONG 値 0 の整数値を 0 xffffffff にことが前提としているプロパティがあります。 複雑なプロパティは、配列や構造体の値があります。

プロパティ記述子と上記のプロパティ値は、記載されているインスタンス仕様および操作データのバッファーのプロパティに固有のバージョン[KS プロパティ、イベント、およびメソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)します。

プロパティ要求は、次のフラグのいずれかの関数を使用して、プロパティに対して実行される操作を指定します。

-   KSPROPERTY\_型\_BASICSUPPORT

-   KSPROPERTY\_型\_取得

-   KSPROPERTY\_型\_設定

フィルターと暗証番号 (pin) のすべてのオブジェクトは、それらのプロパティを basic サポート操作をサポートします。 サポートされるかどうか、*取得*と*設定*操作は、プロパティによって異なります。 フィルターまたは pin オブジェクトの固有の機能を表すプロパティは、get 操作のみを必要とする可能性があります。 構成可能な設定を表すプロパティは、取得操作が現在の設定を読み取るために役立つ可能性もが、設定操作のみを必要があります。 DVD デコーダーのプロパティで、get、セット、および操作を basic サポートを使用する方法の詳細については、次を参照してください。 [KS プロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)します。

プロパティは、クエリまたはストリームの側面を変更します。 DVD デコーダーでは、いくつかのプロパティ セットが使用されます。 このトピックで説明したプロパティ セットにさらに設定 DVD 著作権保護プロパティをサポートしてすべての DVD デコーダーの入力ストリーム

すべてのプロパティの説明には、DVD デコーダー ミニドライバーが読み取りまたは書き込みのプロパティをサポートするために必要かどうかを示すテーブルが含まれています。 DVD デコーダー ミニドライバーは、状態を返す必要があります\_いない\_を取得または設定、ミニドライバーでサポートされていないプロパティに対する要求の応答ではサポートされています。

DVD デコーダー ミニドライバーは、次のプロパティのセットが定義されています。

[KSPROPSETID\_AudioDecoderOut](kspropsetid-audiodecoderout.md)

[KSPROPSETID\_DvdSubPic](kspropsetid-dvdsubpic.md)

[KSPROPSETID\_CopyProt](kspropsetid-copyprot.md)

[KSPROPSETID\_TSRateChange](kspropsetid-tsratechange.md)

[KSPROPSETID\_VPConfig と KSPROPSETID\_VPVBIConfig](kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig.md)

[KSPROPSETID\_Wave](kspropsetid-wave.md)

 

 





