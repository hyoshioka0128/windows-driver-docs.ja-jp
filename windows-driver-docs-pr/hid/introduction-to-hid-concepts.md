---
title: HID の概念の概要
description: このセクションでは、ヒューマン インターフェイス デバイス (HID) が導入されています。 通常、これらは、人間が直接コンピューター システムの動作の制御に使用するデバイスです。
ms.assetid: 477FF911-5A17-4EA5-9403-1D7B4E8B3BA5
keywords:
- '[ヒューマン インターフェイス デバイス]'
- HID
- キーボード
- マウス
- 感覚データ
- 加速度計
- ジャイロスコープなどがあります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b30948cea3a3d07b29e1f1843ff683fe11194e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553676"
---
# <a name="introduction-to-hid-concepts"></a>HID の概念の概要


このセクションでは、ヒューマン インターフェイス デバイス (HID) が導入されています。 通常、これらは、人間が直接コンピューター システムの動作の制御に使用するデバイスです。

## <a name="history-of-hid"></a>HID の履歴


HID の定義は、USB 経由でのデバイス クラスとして開始します。 その時点での目標は、ps/2 に交換を定義し、キーボード、マウス、およびゲーム コント ローラーなどの HID デバイスに対して、汎用ドライバーの作成を許可している USB 経由でインターフェイスを作成するでした。 HID、前に、デバイスは、マウスとキーボードの厳密に定義されたプロトコルに準拠する必要があります。 すべてのハードウェア技術革新には、既存のプロトコルでのデータの使用、または独自のドライバーに必要な非標準のハードウェアのオーバー ロードが必要でした。 HID のビジョンは、オペレーティング システムで「モードで起動」デバイスの基本的なサポートを提供することが、簡単にプログラミング可能な拡張可能な標準化されたインターフェイスとの差別化を提供するハードウェアのベンダーを許可する方法を見つけることを開始します。

今日では、HID デバイスが含まれます。 英数字表示、バーコード リーダー、スピーカー/ヘッドセット、補助ディスプレイ、センサー、および MRI (はい、入院期間) 上のボリューム コントロール。 さらに、多くのハードウェア ベンダは、自社独自のデバイス用 HID を使用します。

HID は USB 経由で開始されましたが、最初からバスに依存しない方法で設計されました。 低待機時間向けに設計されていた、低帯域幅のデバイスが、柔軟性が高く、および、レートが基になるトランスポートによって指定されています。 1990 年代後半、承認された HID USB 経由での仕様とその後すぐに開始する追加のトランスポート経由でサポートします。 今日では、HID では、標準のプロトコルを持つ複数のトランスポートで、次のトランスポートのサポートは HID for Windows 8 でネイティブ。

-   USB
-   Bluetooth
-   Bluetooth LE
-   I²C

ベンダーの特定のトランスポートは、サード パーティ ベンダー固有のトランスポートのドライバーを使用しても許可されます。 詳細については、以降のセクションで提供されます。

## <a name="hid-concepts"></a>HID の概念


HID は、いくつかの基本的な概念、レポート記述子、およびレポートの上に構築します。 レポートは、デバイスとソフトウェア クライアントの間で交換される実際のデータの blob です。 レポート記述子では、形式とサポートされるデータの各 blob の意味について説明します。

### <a name="reports"></a>レポート

アプリケーションと HID デバイスは、データを交換して、ときに、これはレポートを通じて実行されます。 次の 3 つのレポートの種類があります。出力は次のレポート、レポートを入力し、レポートの機能します。

| レポートの種類    | 説明                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------|
| 入力のレポート   | データの blob に送信される、HID デバイスから、アプリケーションでは、通常、コントロールの状態が変更されたとき。 |
| レポートの出力  | キーボードの Led をたとえば、HID デバイスにアプリケーションから送信されるデータの blob。         |
| 機能のレポート | データの blob を手動で読み取りや書き込みをすることができます、通常の構成情報に関連します。    |

 

レポート記述子で定義されている各上位レベルのコレクションがゼロ (0) を含めることができます、または各型の他のレポート。

### <a name="usage-tables"></a>使用状況テーブル

HID のグループの操作では、HID Usage Tables を構成するドキュメントのセットを公開します。 これは、実質的に、HID デバイスに許可するについて説明しているディクショナリです。 これらの非表示に使用状況テーブルには、使用法の説明を伴う一覧が含まれます。 使用方法は、目的の意味と特定のレポート記述子で説明されている項目の使用について、アプリケーション開発者に情報を提供します。 たとえば、マウスの左ボタンに対して定義されている使用量があります。 レポートでアプリケーションをどこにマウスの左ボタンの現在の状態レポート記述子を定義できます。 使用状況テーブルは、[使い方] ページと呼ばれるいくつかの名前空間に分割されます。 使用状況の各ページには、一連のドキュメントを整理するために関連する使用状況について説明します。 使用状況 ページと使用状況の組み合わせでは、使用状況テーブル内の特定の使用を一意に識別する使用状況の ID を定義します。

## <a name="the-hid-application-programming-interface-api"></a>HID アプリケーション プログラミング インターフェイス (API)


HID の Api の 3 つのカテゴリがあります。 デバイスの検出とセットアップ、データの移動、およびレポートの作成/解釈します。

### <a name="device-discovery-and-setup"></a>デバイスの検出とセットアップ

次の一覧を使用できるアプリケーションを非表示に API を識別します。 そのデバイスと通信を確立すると、HID デバイスのプロパティを識別します。 さらに、アプリケーションできますを使用して、これらの API のいくつかの上位レベルのコレクションを識別します。

-   [**HidD\_GetAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff538900)
-   [**HidD\_GetHidGuid**](https://msdn.microsoft.com/library/windows/hardware/ff538924)
-   [**HidD\_GetIndexedString**](https://msdn.microsoft.com/library/windows/hardware/ff538927)
-   [**HidD\_GetManufacturerString**](https://msdn.microsoft.com/library/windows/hardware/ff538959)
-   [**HidD\_GetPhysicalDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff539677)
-   [**HidD\_GetPreparsedData**](https://msdn.microsoft.com/library/windows/hardware/ff539679)
-   [**HidD\_GetProductString**](https://msdn.microsoft.com/library/windows/hardware/ff539681)
-   [**HidD\_GetSerialNumberString**](https://msdn.microsoft.com/library/windows/hardware/ff539683)
-   [**HidD\_GetNumInputBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff539675)
-   [**HidD\_SetNumInputBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff539686)

### <a name="data-movement"></a>データの移動

アプリケーションは、アプリと、選択したデバイスの間でデータを前後へ移動に使用できる非表示に API を次に示します。

-   [**HidD\_GetInputReport**](https://msdn.microsoft.com/library/windows/hardware/ff538945)
-   [**HidD\_SetFeature**](https://msdn.microsoft.com/library/windows/hardware/ff539684)
-   [**HidD\_SetOutputReport**](https://msdn.microsoft.com/library/windows/hardware/ff539690)
-   [ReadFile](https://msdn.microsoft.com/library/windows/desktop/aa365467.aspx)
-   [WriteFile](https://msdn.microsoft.com/library/windows/desktop/aa365747.aspx)

### <a name="report-creation-and-interpretation"></a>レポートの作成と解釈

独自のハードウェア用 HID アプリを作成する場合、サイズと、デバイスによって発行された各レポートの形式の既存の知識があること。 この場合、入力をキャストし、出力構造体にバッファーをレポートしてとデータを使用するアプリができますとします。

ただし、一般的な機能 (再生ボタンが押されたときを検出する必要があるミュージック アプリなど) を公開するすべてのデバイスと通信する HID アプリを作成する場合、わからない HID レポートの形式とサイズ。 このカテゴリのアプリケーションは、上位レベルの特定のコレクションと特定の使用法を理解しています。

アプリケーションにレポート記述子を活用して、および特定の使用は、レポートでは、(可能性がある) の値の単位である場所を判別するために必要なデバイスから受信したレポートを解釈するために、または送信されるレポートを作成するには、レポートします。 これは、HID 解析が必要です。 Windows では、ドライバーおよびアプリケーション用 HID パーサーを提供します。 このパーサーは、一連の Api を公開します (HidP\_\*) デバイスでサポートされている使用法の種類を検出、レポートでは、このような使用状況の状態を判断するまたはデバイスでの使用状況の状態を変更するレポートの作成を使用できます。

HID パーサー Api を次に示します。

-   [**HidP\_GetButtonCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539707)
-   [**HidP\_GetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539708)
-   [**HidP\_GetButtonsEx**](https://msdn.microsoft.com/library/windows/hardware/ff539712)
-   [**HidP\_GetCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539715)
-   [**HidP\_GetData**](https://msdn.microsoft.com/library/windows/hardware/ff539718)
-   [**HidP\_GetExtendedAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff539721)
-   [**HidP\_GetLinkCollectionNodes**](https://msdn.microsoft.com/library/windows/hardware/ff539725)
-   [**HidP\_GetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539729)
-   [**HidP\_GetSpecificButtonCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539733)
-   [**HidP\_GetSpecificValueCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539737)
-   [**HidP\_GetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539742)
-   [**HidP\_GetUsagesEx**](https://msdn.microsoft.com/library/windows/hardware/ff539745)
-   [**HidP\_GetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539748)
-   [**HidP\_GetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539750)
-   [**HidP\_GetValueCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539754)
-   [**HidP\_InitializeReportForID**](https://msdn.microsoft.com/library/windows/hardware/ff539757)
-   [**HidP\_IsSameUsageAndPage**](https://msdn.microsoft.com/library/windows/hardware/ff539761)
-   [**HidP\_MaxDataListLength**](https://msdn.microsoft.com/library/windows/hardware/ff539768)
-   [**HidP\_MaxUsageListLength**](https://msdn.microsoft.com/library/windows/hardware/ff539770)
-   [**HidP\_SetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539779)
-   [**HidP\_setdata メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff539783)
-   [**HidP\_SetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539787)
-   [**HidP\_SetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539792)
-   [**HidP\_SetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539797)
-   [**HidP\_SetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539801)
-   [**HidP\_UnsetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539812)
-   [**HidP\_UnsetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539819)
-   [**HidP\_UsageAndPageListDifference**](https://msdn.microsoft.com/library/windows/hardware/ff539824)
-   [**HidP\_UsageListDifference**](https://msdn.microsoft.com/library/windows/hardware/ff539826)

 

 




