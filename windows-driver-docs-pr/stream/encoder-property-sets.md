---
title: エンコーダーのプロパティ セット
description: エンコーダーのプロパティ セット
ms.assetid: b273464d-0d40-488c-a848-291f949609f0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ed4485ba5eec89b0939ee305284bb271f57dc2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578828"
---
# <a name="encoder-property-sets"></a>エンコーダーのプロパティ セット


## <span id="ddk_encoder_property_sets_ks"></span><span id="DDK_ENCODER_PROPERTY_SETS_KS"></span>


このセクションでは、エンコーダーおよび Microsoft Windows 98 で WDM カーネル ストリーミング サービスを使用するエンコーダー ミニドライバーで利用可能なコーデック API に固有のプロパティ セットについて説明します。/Me、Windows 2000、および Windows XP 以降。

各プロパティのリファレンス ページには、次のような列見出しのテーブルが含まれています。


| 取得 | Set | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

これらの見出しには、次の意味があります。

-   **取得**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_プロパティの GET 要求ですか?

-   **設定**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_セット プロパティ要求でしょうか。

-   **ターゲット**

    これは、どのプロパティに要求が送信された KS オブジェクトです。 ビデオ エンコーダー プロパティの対象は、フィルターまたは pin のいずれかです。 (プロパティ要求を指定します、ターゲット オブジェクトがカーネル ハンドルによって。)

-   **プロパティ記述子の型**

    プロパティ記述子には、プロパティとそのプロパティに対して実行する操作を指定します。 記述子は常に始まり、 [ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)構造体。

-   **プロパティ値の型**

    プロパティの値を持つし、この値の型は、プロパティによって異なります。 たとえば、オンまたはオフ----だけ 2 つの状態のいずれかの可能性のあるプロパティには、ブール値通常があります。 ULONG 値 0x0 からの整数値を 0 xffffffff にことが前提としているプロパティがあります。 複雑なプロパティは、配列や構造体の値があります。

プロパティ記述子と上記のプロパティ値は、記載されているインスタンス仕様および操作データのバッファーのプロパティに固有のバージョン[KS プロパティ、イベント、およびメソッド](https://msdn.microsoft.com/library/windows/hardware/ff567673)します。

プロパティ要求は、次のフラグのいずれかの関数を使用して、プロパティに対して実行される操作を指定します。

-   KSPROPERTY\_型\_BASICSUPPORT

-   KSPROPERTY\_型\_取得

-   KSPROPERTY\_型\_設定

フィルターと暗証番号 (pin) のすべてのオブジェクトは、それらのプロパティを basic サポート操作をサポートします。 サポートされるかどうか、*取得*と*設定*操作は、プロパティによって異なります。 フィルターまたは pin オブジェクトの固有の機能を表すプロパティにのみ必要になる可能性は、*取得*操作。 構成可能な設定を表すプロパティの必要がありますのみ、*設定*操作が、*取得*操作が現在の設定を読み取るために役立つ可能性も。 ビデオ エンコーダーのプロパティで、get、セット、および操作を basic サポートを使用する方法の詳細については、[KS プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff567671)を参照してください。

すべてのプロパティの説明内のテーブルでは、ビデオ エンコーダー ミニドライバーが読み取りまたは書き込みのプロパティをサポートするために必要かどうかを示します。 ビデオ エンコーダー ミニドライバーは、状態を返す必要があります\_いない\_を取得または設定、ミニドライバーでサポートされていないプロパティに対する要求の応答ではサポートされています。

次のプロパティ セットごとには、ビデオ エンコーダー ミニドライバーが実装する必要を 1 つのプロパティが含まれます。 つまり、各プロパティが独自のセットを取得効果的に、そのために 0 を指定、 **PropertyId**のメンバー、 [ **KSPROPERTY\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff565176) でメンバー[ **KSPROPERTY\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff565617)必要に応じて構造体します。

次のプロパティ セットは、コーデック API に属します。

[CODECAPI\_ビデオ\_エンコーダー](codecapi-video-encoder.md)

[CODECAPI\_オーディオ\_エンコーダー](codecapi-audio-encoder.md)

[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)

[CODECAPI\_SUPPORTSEVENTS](codecapi-supportsevents.md)

[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)

次のプロパティ セットは、エンコーダー API に属します。

[ENCAPIPARAM\_ビットレート](encapiparam-bitrate.md)

[ENCAPIPARAM\_ビットレート\_モード](encapiparam-bitrate-mode.md)

[ENCAPIPARAM\_ピーク\_ビットレート](encapiparam-peak-bitrate.md)

 

 





