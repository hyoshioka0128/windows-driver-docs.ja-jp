---
title: オーディオのプロパティの要求
description: オーディオのプロパティの要求
ms.assetid: dcfd139c-fca3-4068-8324-aa2c952dbc1f
keywords:
- オーディオプロパティ WDK、要求
- WDM オーディオプロパティ WDK、要求
- WDK オーディオ、プロパティ要求をフィルター処理します
- ノード WDK オーディオ、プロパティ要求
- WDK オーディオ、プロパティ要求をピン留めする
- KS WDK オーディオ、プロパティ要求をフィルター処理します
- 過剰指定の要求 WDK オーディオ
- 指定されていない要求の WDK オーディオ
- WDK オーディオ、記述子をフィルター処理します
- プロパティが WDK オーディオを要求する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81a16c49be28699d2619f6929c25fc8be8bbdcfa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831327"
---
# <a name="audio-property-requests"></a>オーディオのプロパティの要求


## <span id="audio_property_requests"></span><span id="AUDIO_PROPERTY_REQUESTS"></span>


Microsoft Windows Driver Model (WDM) オーディオドライバーのクライアントは、ks[プロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)の要求を ks フィルターに送信し、ドライバーがインスタンス化したことをピン留めすることができます。 たとえば、ユーザーモードクライアントは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出すことによって、ks プロパティ要求を送信できます (Microsoft Windows SDK のドキュメントを参照してください)。これには、IOCTL\_KS\_プロパティの i/o 制御コードが含まれます。 この関数は、プロパティ要求を含む IRP を、指定されたフィルターまたは pin オブジェクトに送信します。

オーディオドライバーは、プロパティ (KSK プロパティ\_TYPE\_GET、KSK プロパティ\_TYPE\_SET、および KSK プロパティ\_BASICSUPPORT) に対する get、set、および basic サポート要求をサポートしています。 詳細については、「[オーディオドライバーのプロパティセット](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)」を参照してください。

クライアントは、フィルタープロパティ、ピンプロパティ、ノードプロパティの3種類のプロパティに対して要求を送信できます。 詳細については、「[フィルター、ピン、およびノードのプロパティ](filter--pin--and-node-properties.md)」を参照してください。

フィルタープロパティ要求をフィルターオブジェクトに送信すると、クライアントはそのインスタンスハンドルによってターゲットフィルターを指定します (「[フィルターファクトリ](filter-factories.md)」を参照してください)。 同様に、pin オブジェクトにピンプロパティ要求を送信する場合、ターゲットピンはそのインスタンスハンドルによって指定されます (「[ピンファクトリ](pin-factories.md)」を参照してください)。 どちらの種類の要求にも、次の値を指定する[**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体が含まれています。

-   プロパティセットを識別する GUID

-   指定されたプロパティセット内のプロパティ項目を識別するインデックス。

-   プロパティ要求の種類 (get、set、または basic サポート) を示すフラグ

関連するプロパティは、プロパティセットを形成するためにまとめて収集されます。 特定のプロパティは、そのプロパティセットと、そのセット内での位置を指定するインデックスによって識別されます。

ノードプロパティ要求には、 [**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)構造体が含まれています。これは、ksk プロパティ構造とノード ID を結合したものです。 ノードプロパティに応じて、プロパティ要求のターゲットは、フィルターインスタンスまたは pin インスタンスのいずれかになります。

フィルターで特定のノード型の複数のインスタンスを作成できる場合、要求のターゲットはピンハンドルによって指定されます。 ハンドルは、ノードインスタンスが存在するデータパスの先頭または末尾にある pin インスタンスを識別します。 SUM または MUX ノードを含むフィルター (「 [**KSNODETYPE\_SUM**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum) and [**KSNODETYPE\_mux**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux)」を参照) の場合は、次の規則が適用されます。

-   プロパティが、シンク (入力) ピンから下流にあるノードや、SUM または MUX ノードから上流にあるノードに属している場合、プロパティ要求はシンク pin に送信されます。

-   プロパティが、SUM または MUX ノードから下流にあり、ソース (出力) ピンから上流にあるノードに属している場合は、プロパティ要求がソースピンに送信されます。 (また、SUM または MUX ノードのプロパティ要求がソースピンに送信されます)。

これらの規則により、特定のデータパスの特定のノードを一意に識別できます。

ミキサー API を使用してデータパス内のノードを走査する方法の詳細については、「 [Kernel Streaming Topology To Audio MIXER Api Translation](kernel-streaming-topology-to-audio-mixer-api-translation.md)」を参照してください。

 

 




