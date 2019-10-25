---
title: HID の概念の紹介
description: このセクションでは、ヒューマン インターフェイス デバイス (HID) について紹介します。 通常、これらは、人間がコンピューター システムの操作を直接制御するために使用するデバイスです。
ms.assetid: 477FF911-5A17-4EA5-9403-1D7B4E8B3BA5
keywords:
- '[ヒューマン インターフェイス デバイス]'
- HID
- キーボード
- マウス
- データの sensory
- 加速度計
- ジャイロスコープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19cb06057b4cb9708cd87787a0b6b3c523b17be7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841576"
---
# <a name="introduction-to-hid-concepts"></a>HID の概念の紹介


このセクションでは、ヒューマン インターフェイス デバイス (HID) について紹介します。 通常、これらは、人間がコンピューター システムの操作を直接制御するために使用するデバイスです。

## <a name="history-of-hid"></a>HID の履歴


USB 経由でデバイスクラスとして開始された HID の定義。 この時点での目標は、PS/2 に代わるものを定義し、USB 経由のインターフェイスを作成して、キーボード、マウス、ゲームコントローラーなどの HID デバイス用の汎用ドライバーを作成できるようにすることでした。 HID より前は、デバイスは、マウスとキーボードに対して厳密に定義されたプロトコルに準拠している必要がありました。 すべてのハードウェアイノベーションは、既存のプロトコルでのデータの使用の過負荷、または独自のドライバーを必要とする標準以外のハードウェアの作成を必要としています。 HID のビジョンは、オペレーティングシステムでこれらの "ブートモード" デバイスの基本的なサポートを提供すると同時に、ハードウェアベンダーが拡張可能で標準化された、簡単にプログラミング可能なインターフェイスと区別できるようにする方法を発見しました。

現在、HID デバイスには、英数字表示、バーコードリーダー、スピーカー/ヘッドセットのボリュームコントロール、補助ディスプレイ、センサー、MRI (はい、病院) が含まれています。 また、多くのハードウェアベンダーは、独自のデバイスに対して HID を使用します。

HID は USB 経由で開始されましたが、最初からバスに依存しない方法で設計されていました。 このように設計されているのは、待機時間が短く、帯域幅が狭いデバイスですが、柔軟性があり、基になるトランスポートによってレートが指定されているためです。 USB 経由の HID の仕様は、1990年代後半に批准され、その後すぐに開始される追加のトランスポートをサポートしていました。 現在、HID には複数のトランスポートに対する標準プロトコルがあり、HID の Windows 8 では次のトランスポートがネイティブでサポートされています。

-   [USB]
-   [Bluetooth]
-   Bluetooth LE
-   I ² C

ベンダー固有のトランスポートは、サードパーティベンダー固有のトランスポートドライバー経由でも許可されます。 詳細については、後のセクションで説明します。

## <a name="hid-concepts"></a>HID の概念


HID は、いくつかの基本的な概念、レポート記述子、およびレポートに基づいて構築されています。 レポートは、デバイスとソフトウェアクライアントの間で交換される実際のデータ blob です。 レポート記述子は、サポートする各データ blob の形式と意味を記述します。

### <a name="reports"></a>レポート

アプリケーションと HID デバイスがデータを交換するときは、レポートを使用して行います。 レポートの種類には、入力レポート、出力レポート、機能レポートの3種類があります。

| レポートの種類    | 説明                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------|
| 入力レポート   | 通常、コントロールの状態が変化したときに、HID デバイスからアプリケーションに送信されるデータ blob。 |
| 出力レポート  | たとえば、キーボードの Led に対して、アプリケーションから HID デバイスに送信されるデータ blob。         |
| 機能レポート | データ blob は、手動で読み書きすることができ、通常は構成情報に関連します。    |

 

レポート記述子に定義されている各最上位レベルのコレクションには、各型の0個以上のレポートを含めることができます。

### <a name="usage-tables"></a>使用状況テーブル

HID の作業グループは、HID の使用状況テーブルを構成する一連のドキュメントを公開します。 これは、実際には、どのような HID デバイスが許可されているかを説明するディクショナリです。 これらの HID 使用状況テーブルには、使用法の説明が記載された一覧が含まれています。 を使用すると、アプリケーションの開発者に、レポート記述子に記述されている特定の項目の意味と使用方法についての情報が提供されます。 たとえば、マウスの左ボタンに定義されている使用法があります。 レポート記述子では、アプリケーションがマウスの左ボタンの現在の状態を見つけることができるレポート内の場所を定義できます。 使用状況テーブルは、使用状況ページと呼ばれる複数の名前空間に分割されます。 各 [使用状況] ページには、ドキュメントを整理するのに役立つ、関連する使用法のセットが記述されています。 使用状況ページと使用状況の組み合わせによって、使用状況テーブルの特定の使用状況を一意に識別する使用 ID が定義されます。

## <a name="the-hid-application-programming-interface-api"></a>HID アプリケーションプログラミングインターフェイス (API)


HID Api には、デバイスの検出とセットアップ、データの移動、レポートの作成/解釈という3つのカテゴリがあります。

### <a name="device-discovery-and-setup"></a>デバイスの検出とセットアップ

次のリストは、アプリケーションが HID デバイスのプロパティを識別し、そのデバイスとの通信を確立するために使用できる HID API を示しています。 さらに、アプリケーションでは、これらの API の一部を使用して、最上位レベルのコレクションを識別できます。

-   [**HidD\_GetAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getattributes)
-   [**HidD\_GetHidGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid)
-   [**HidD\_GetIndexedString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getindexedstring)
-   [**HidD\_GetManufacturerString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getmanufacturerstring)
-   [**HidD\_GetPhysicalDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getphysicaldescriptor)
-   [**HidD\_GetPreparsedData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)
-   [**HidD\_GetProductString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getproductstring)
-   [**HidD\_GetSerialNumberString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getserialnumberstring)
-   [**HidD\_GetNumInputBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getnuminputbuffers)
-   [**HidD\_SetNumInputBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setnuminputbuffers)

### <a name="data-movement"></a>データの移動

次の一覧は、アプリケーションがアプリと選択したデバイスの間でデータを移動するために使用できる HID API を示しています。

-   [**HidD\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)
-   [**HidD\_SetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature)
-   [**HidD\_SetOutputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport)
-   [ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)
-   [WriteFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)

### <a name="report-creation-and-interpretation"></a>レポートの作成と解釈

独自のハードウェア用に HID アプリを作成する場合は、デバイスによって発行された各レポートのサイズと形式に関する知識を既に持っています。 この場合、アプリは、入力および出力レポートのバッファーを構造体にキャストし、データを使用できます。

ただし、一般的な機能を公開するすべてのデバイスと通信する HID アプリを作成する場合 (たとえば、再生ボタンが押されたときに検出する必要がある音楽アプリ)、HID レポートのサイズと形式がわからない場合があります。 このカテゴリのアプリケーションは、特定の最上位レベルのコレクションと特定の使用状況を認識します。

デバイスから受信したレポートを解釈したり、送信するレポートを作成したりするには、アプリケーションでレポート記述子を利用して、レポートに特定の使用状況があるかどうか、および (場合によっては) の値の単位を確認する必要があります。reports. ここで、HID 解析が必要です。 Windows には、ドライバーとアプリケーションで使用する HID パーサーが用意されています。 このパーサーは、デバイスでサポートされている使用法の種類を検出するために使用できる一連の Api (HidP\_\*) を公開します。また、レポート内での使用状況の状態を判断したり、デバイスの使用状況の状態を変更するためのレポートを作成したりするために使用できます。

次の一覧は、HID パーサー Api を示しています。

-   [**HidP\_GetButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)
-   [**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_GetButtonsEx**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps)
-   [**HidP\_GetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)
-   [**HidP\_GetExtendedAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getextendedattributes)
-   [**HidP\_GetLinkCollectionNodes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getlinkcollectionnodes)
-   [**HidP\_Get/Edの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)
-   [**HidP\_Get固有の Buttoncaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificbuttoncaps)
-   [**HidP\_GetSpecificValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificvaluecaps)
-   [**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)
-   [**HidP\_Getの性別**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)
-   [**HidP\_Getの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)
-   [**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)
-   [**HidP\_GetValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)
-   [**HidP\_初期化 Ereportforid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_initializereportforid)
-   [**HidP\_Issameの場合とページ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_usage_and_page)
-   [**HidP\_Maxdat/Stlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxdatalistlength)
-   [**HidP\_Max使い方 Listlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength)
-   [**HidP\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_SetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)
-   [**HidP\_Setスケール Edの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)
-   [**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)
-   [**HidP\_Setの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)
-   [**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)
-   [**HidP\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
-   [**HidP\_の使い方 Andpagelist減法**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))
-   [**HidP\_の使い方 List相違点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)

 

 




