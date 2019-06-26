---
title: オーディオのプロパティの要求
description: オーディオのプロパティの要求
ms.assetid: dcfd139c-fca3-4068-8324-aa2c952dbc1f
keywords:
- WDK、要求のオーディオのプロパティ
- WDM オーディオ プロパティ WDK、要求
- プロパティ要求 WDK のオーディオをフィルター処理します。
- ノードの WDK オーディオ、プロパティの要求
- ピン WDK オーディオでは、プロパティを要求します。
- KS フィルター WDK オーディオ、プロパティの要求
- overspecified 要求 WDK オーディオ
- 選ば要求 WDK オーディオ
- WDK のオーディオ、記述子のフィルター処理します。
- プロパティ要求 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ab33e12650ed7a04f1e4e5a2e6b939b49de891c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355653"
---
# <a name="audio-property-requests"></a>オーディオのプロパティの要求


## <span id="audio_property_requests"></span><span id="AUDIO_PROPERTY_REQUESTS"></span>


Microsoft Windows Driver Model (WDM) オーディオ ドライバーのクライアント要求を送信できる[KS プロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)KS フィルターと pin をドライバーがインスタンス化します。 ユーザー モードのクライアントが呼び出して KS プロパティの要求を送信するなど、 [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) IOCTL、O コントロール コード (Microsoft Windows SDK のドキュメントを参照してください) を関数\_KS\_プロパティ。 この関数は、指定したフィルターまたは pin オブジェクトにプロパティの要求を含む IRP を送信します。

オーディオ ドライバーのプロパティの get、セット、および basic サポート要求をサポート (KSPROPERTY\_型\_GET、KSPROPERTY\_型\_セット、および KSPROPERTY\_型\_BASICSUPPORT)。 詳細については、次を参照してください。[オーディオ ドライバーのプロパティ セット](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)します。

クライアントは、プロパティの 3 種類の要求を送信できます。 プロパティ、pin のプロパティ、およびノードのプロパティをフィルター処理します。 詳細については、次を参照してください。[フィルター、Pin、およびノードのプロパティ](filter--pin--and-node-properties.md)します。

クライアントがそのインスタンス ハンドルによってターゲット フィルターを指定するフィルター オブジェクトにフィルター プロパティの要求を送信するときに (を参照してください[フィルター ファクトリ](filter-factories.md))。 同様に、暗証番号 (pin) のオブジェクトにピン留めするプロパティの要求を送信するときにターゲットの暗証番号 (pin) がそのインスタンスのハンドルで指定された (を参照してください[Pin ファクトリ](pin-factories.md))。 要求のいずれかの型が含まれています、 [ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))次を指定する構造体。

-   プロパティ セットを識別する GUID

-   指定したプロパティ内のプロパティ項目を識別する、インデックスの設定

-   プロパティ要求 (get、セット、または basic サポート) の種類を示すフラグ

関連するプロパティがまとめて収集プロパティをフォームに設定します。 特定のプロパティは、そのセット内の位置を指定するインデックスとそのプロパティ セットによって識別されます。

ノード プロパティの要求に含まれる、 [ **KSNODEPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty) KSPROPERTY 構造体とノードの ID を組み合わせた構造体 ノードのプロパティに応じてプロパティ要求のターゲットは、フィルター インスタンスまたは暗証番号 (pin) のインスタンスです。

フィルターが特定のノード型の 1 つ以上のインスタンスを作成する場合、要求のターゲットは、暗証番号 (pin) のハンドルによって指定されます。 ハンドルは、先頭またはノード インスタンスが存在するデータ パスの末尾に暗証番号 (pin) のインスタンスを識別します。 SUM や MUX ノードを含むフィルターの場合 (を参照してください[ **KSNODETYPE\_合計**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)と[ **KSNODETYPE\_MUX** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux))、次の規則が適用されます。

-   シンク (入力) の暗証番号 (pin) のダウン ストリームと、合計または MUX ノードから上位にあるノードのプロパティが属している場合、プロパティの要求は、シンクの暗証番号 (pin) に送信されます。

-   プロパティは、合計または MUX ノードのダウン ストリームとソース (出力) の暗証番号 (pin) の上流にあるノードに属している場合、プロパティの要求は、ソースの暗証番号 (pin) に送信されます。 (また、合計または MUX ノードのプロパティの要求に送信されますソースの暗証番号 (pin)。)

これらの規則を特定のデータ パス上の特定のノードを一意に識別できます。

ミキサー API を使用して、データ パスのノードを走査する方法については、次を参照してください。[オーディオ Mixer API 翻訳にカーネル ストリーミング トポロジ](kernel-streaming-topology-to-audio-mixer-api-translation.md)します。

 

 




