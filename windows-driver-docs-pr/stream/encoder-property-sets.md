---
title: エンコーダーのプロパティ セット
description: エンコーダーのプロパティ セット
ms.assetid: b273464d-0d40-488c-a848-291f949609f0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30889d8645ee09aa3be784218f2cb71ab9851c54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834427"
---
# <a name="encoder-property-sets"></a>エンコーダーのプロパティ セット


## <span id="ddk_encoder_property_sets_ks"></span><span id="DDK_ENCODER_PROPERTY_SETS_KS"></span>


このセクションでは、Microsoft Windows 98/Me、Windows 2000、および Windows XP 以降で WDM カーネルストリーミングサービスを使用する encoder ミニドライバーで使用できるエンコーダーとコーデックに固有のプロパティセットについて説明します。

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

    これは、プロパティ要求が送信される KS オブジェクトです。 Video encoder プロパティのターゲットは、フィルターまたは pin です。 (プロパティ要求では、カーネルハンドルによってターゲットオブジェクトが指定されます)。

-   **プロパティ記述子の型**

    プロパティ記述子は、プロパティと、そのプロパティに対して実行する操作を指定します。 記述子は常に[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)構造で始まります。

-   **プロパティ値の型**

    プロパティには値があり、この値の型はプロパティによって異なります。 たとえば、2つの状態 (on または off) のいずれかであるプロパティは、通常、ブール値を持ちます。 0x0 から0xFFFFFFFF の整数値を想定できるプロパティは、ULONG 値を持つ場合があります。 より複雑なプロパティには、配列または構造体の値が含まれる場合があります。

上記のプロパティ記述子とプロパティ値は、 [「KS プロパティ、イベント、およびメソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)」で説明されている、インスタンス仕様および操作データバッファーのプロパティ固有バージョンです。

プロパティ要求では、次のいずれかのフラグを使用して、プロパティに対して実行する操作を指定します。

-   KSPROPERTY\_TYPE\_BASICSUPPORT

-   KSK プロパティ\_TYPE\_GET

-   KSK プロパティ\_TYPE\_SET

すべてのフィルターオブジェクトとピンオブジェクトは、そのプロパティに対する基本サポート操作をサポートしています。 *Get*操作と*Set*操作をサポートするかどうかは、プロパティによって異なります。 Filter オブジェクトまたは pin オブジェクトの固有の機能を表すプロパティは、 *get*操作のみを必要とする可能性があります。 構成可能な設定を表すプロパティは、*設定*操作のみを必要とする場合がありますが、 *get*操作は現在の設定の読み取りにも便利な場合があります。 ビデオエンコーダーのプロパティで get、set、および basic サポート操作を使用する方法の詳細については、「 [KS のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)」を参照してください。

すべてのプロパティの説明に含まれるテーブルは、プロパティの読み取りまたは書き込みをサポートするために video encoder ミニドライバーが必要かどうかを示します。 Video encoder ミニドライバーは、ミニドライバーによってサポートされていないプロパティの取得または設定要求に応答して、サポートされて\_いない状態\_返す必要があります。

次のプロパティセットには、video encoder ミニドライバーによって実装される必要がある1つのプロパティが含まれています。 つまり、実質的に各プロパティが独自のセットを取得します。そのため、必要に応じて、 [**Ksk プロパティ\_set**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)構造体[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)の**PropertyId**メンバーに0を指定します。

次のプロパティセットは、コーデック API に属しています。

[CODECAPI\_VIDEO\_ENCODER](codecapi-video-encoder.md)

[CODECAPI\_AUDIO\_ENCODER](codecapi-audio-encoder.md)

[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)

[CODECAPI\_SUPPORTSEVENTS](codecapi-supportsevents.md)

[CODECAPI\_CURRENTCHANGELIST リスト](codecapi-currentchangelist.md)

次のプロパティセットは、encoder API に属しています。

[ENCAPIPARAM\_ビットレート](encapiparam-bitrate.md)

[ENCAPIPARAM\_ビットレート\_モード](encapiparam-bitrate-mode.md)

[ENCAPIPARAM\_ピーク\_ビットレート](encapiparam-peak-bitrate.md)

 

 





