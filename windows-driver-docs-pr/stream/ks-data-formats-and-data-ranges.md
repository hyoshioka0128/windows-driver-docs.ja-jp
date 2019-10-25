---
title: KS のデータ形式とデータ範囲
description: KS のデータ形式とデータ範囲
ms.assetid: 44b55a5a-ec58-4c1e-b780-e20829fe3edf
keywords:
- データ形式 WDK カーネルストリーミング
- WDK カーネルストリーミングの形式
- WDK カーネルストリーミングの範囲
- データ範囲 WDK カーネルストリーミング
- KS データ形式 WDK カーネルストリーミング
- KS データ範囲 WDK カーネルストリーミング
- KSDATARANGE 場合
- KSDATAFORMAT
- カーネルストリーミング WDK、データ範囲
- KS WDK、データ範囲
- カーネルストリーミング WDK、データ形式
- KS WDK、データ形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a986ffe5827f08b570ee18641d0991e323ae94ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842520"
---
# <a name="ks-data-formats-and-data-ranges"></a>KS のデータ形式とデータ範囲





KS ピンは、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体と[**ksk datar構造**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))体を使用して、データ形式と範囲を指定します。 データ形式は、データストリームの1つの属性を指定します。たとえば、オーディオサンプリングサイズは16ビットです。 データ範囲では、16-24 ビットのオーディオサンプリング範囲など、複数の形式を指定します。

ミニドライバーには、提供されている各[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造体の ksk datarの構造体の配列が含まれています。 Microsoft が提供する形式は、 *ksmedia. h*で列挙されます。

KSK DATARの構造体には、KSDATAFORMAT 構造体と同じメンバーがあります。ただし、ミニドライバーでは、KSDATARANGE メジャー形式、サブフォーマット、および指定子のメンバーに対してワイルドカード値を指定できます。

ミニドライバーでは、これらの構造の拡張バージョンを使用してメディア固有の値を定義します。 オーディオとビデオのキャプチャのしくみについては、「[オーディオデータ形式とデータ範囲](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-data-formats-and-data-ranges)」および「[ストリーム形式の選択](selecting-a-stream-format.md)」を参照してください。

クライアントは次のプロパティを使用して、フィルターの特定のピンファクトリによってインスタンス化された pin のデータ形式のサポートを照会します。

-   [**Ksk プロパティ\_ピン\_DATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)です。 KS フィルターは、ピンファクトリによってインスタンス化されたピンでサポートされるすべてのデータ範囲を報告します。 これ*には、pin がサポートできる*すべてのデータ形式が含まれます。

-   [**Ksk プロパティ\_ピン\_CONSTRAINEDDATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)です。 KS フィルターは、現在の内部ドライバーの状態を指定して、ピンファクトリによってインスタンス化されたピンでサポートされるすべてのデータ範囲を報告します。

-   [**Ksk プロパティ\_ピン\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)です。 クライアントはこのプロパティを使用して、pin ファクトリによってインスタンス化された pin が特定のデータ形式をサポートしているかどうかを照会できます。

-   [**Ksk プロパティ\_ピン\_DATAINTERSECTION 集合**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)です。 クライアントはこのプロパティを使用して、さまざまなデータ形式を提供できます。

Pin がインスタンス化されると、ユーザーモードクライアントは、現在のデータ形式を判断したり、 [Ksk Propsetid\_接続](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-connection)プロパティ要求を使用してデータ形式の変更を要求したりすることができます。 たとえば、クライアントは、 [**Ksk プロパティ\_接続\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-proposedataformat)を使用して、pin が特定のデータ形式をサポートしているかどうかを判断します。 クライアントは、 [**DATAFORMAT\_接続に Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-dataformat)を使用してデータ形式を変更\_ます。

KS ミニドライバーとクライアントは、データ形式を動的にネゴシエートできます。 ストリームのデータ形式が変更された場合、ミニドライバーは、KSK ストリームの\_ヘッダーの**Optionsflags**メンバー内の\_optionsf\_datadiscontinuity フラグを指定して、ksk ストリーム\_ヘッダーを指定します。 ミニドライバーは、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体で記述された新しいデータ形式を、対応するデータバッファーに渡します。

 

 




