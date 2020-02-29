---
title: HID アプリケーションプログラミングインターフェイス (API)
description: ヒューマンインターフェイスデバイス (HID) API の概要。
ms.assetid: 477FF911-5A17-4EA5-9403-1D7B4E8B3BA5
keywords:
- '[ヒューマン インターフェイス デバイス]'
- HID
- キーボード
- マウス
- データの sensory
- 加速度計
- ジャイロスコープ
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 32617754aa2973bd1c8eac7db62b5c044c086684
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166660"
---
# <a name="hid-application-programming-interface-api"></a>HID アプリケーションプログラミングインターフェイス (API)

HID Api には、デバイスの検出とセットアップ、データの移動、レポートの作成/解釈という3つのカテゴリがあります。

## <a name="device-discovery-and-setup"></a>デバイスの検出とセットアップ

これらの HID Api は、HID デバイスのプロパティを識別し、そのデバイスとの通信を確立するために使用されます。 アプリケーションでは、これらの Api を使用して最上位レベルのコレクションを識別します。

- [HidD\_GetAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getattributes)
- [HidD\_GetHidGuid](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid)
- [HidD\_GetIndexedString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getindexedstring)
- [HidD\_GetManufacturerString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getmanufacturerstring)
- [HidD\_GetPhysicalDescriptor](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getphysicaldescriptor)
- [HidD\_GetPreparsedData](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)
- [HidD\_GetProductString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getproductstring)
- [HidD\_GetSerialNumberString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getserialnumberstring)
- [HidD\_GetNumInputBuffers](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getnuminputbuffers)
- [HidD\_SetNumInputBuffers](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setnuminputbuffers)

## <a name="data-movement"></a>データの移動

これらの HID Api は、アプリケーションと選択されたデバイスの間でデータを移動するために使用されます。

- [HidD\_GetInputReport](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)
- [HidD\_SetFeature](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature)
- [HidD\_SetOutputReport](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport)
- [ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)
- [WriteFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)

## <a name="report-creation-and-interpretation"></a>レポートの作成と解釈

カスタムハードウェアの開発者は、デバイスによって発行された各レポートのサイズと形式を知ることができます。 この場合、アプリケーションは、入力および出力レポートのバッファーを構造体にキャストし、データを使用できます。

一般的な機能を公開するすべてのデバイス (たとえば、再生ボタンが押されたときに検出する必要がある音楽アプリケーション) との通信を目的とした HID アプリケーションの開発者は、HID レポートのサイズと形式がわからない場合があります。 このカテゴリのアプリケーションは、特定の最上位レベルのコレクションと特定の使用状況を認識します。

デバイスから受信したレポートを解釈したり、送信するレポートを作成したりするには、アプリケーションでレポート記述子を利用して、レポート内の特定の使用状況があるかどうか、およびレポート内の値の単位を確認する必要があります。 このような場合は、HID 解析が必要です。 Windows では、Api (HidP\_\*) によって使用される HID パーサーを提供しています。これを使用すると、デバイスでサポートされている使用法の種類を検出したり、レポート内でその使用状況を確認したり、デバイスの使用状況の状態を変更するためのレポートを作成したりできます。

これらは、HID パーサー Api です。

- [HidP\_GetButtonCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)
- [HidP\_GetButtons](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_GetButtonsEx](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_GetCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps)
- [HidP\_GetData](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)
- [HidP\_GetExtendedAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getextendedattributes)
- [HidP\_GetLinkCollectionNodes](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getlinkcollectionnodes)
- [HidP\_Get/Edの値](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)
- [HidP\_Get固有の Buttoncaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificbuttoncaps)
- [HidP\_GetSpecificValueCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificvaluecaps)
- [HidP\_GetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)
- [HidP\_Getの性別](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)
- [HidP\_Getの値](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)
- [HidP\_GetUsageValueArray](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)
- [HidP\_GetValueCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)
- [HidP\_初期化 Ereportforid](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_initializereportforid)
- [HidP\_Issameの場合とページ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_usage_and_page)
- [HidP\_Maxdat/Stlength](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxdatalistlength)
- [HidP\_Max使い方 Listlength](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength)
- [HidP\_SetButtons](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_SetData](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)
- [HidP\_Setスケール Edの値](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)
- [HidP\_SetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)
- [HidP\_Setの値](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)
- [HidP\_SetUsageValueArray](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)
- [HidP\_UnsetButtons](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_UnsetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
- [HidP\_の使い方 Andpagelist減法](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))
- [HidP\_の使い方 List相違点](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)
