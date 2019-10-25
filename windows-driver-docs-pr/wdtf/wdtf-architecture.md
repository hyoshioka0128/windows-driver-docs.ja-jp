---
title: WDTF のアーキテクチャ
description: WDTF のアーキテクチャ
ms.assetid: 8c110e97-6870-41f1-a4f3-4d44b2974c1a
keywords:
- Windows デバイステストフレームワーク WDK、アーキテクチャ
- WDTF WDK、アーキテクチャ
- アーキテクチャ WDK WDTF
- Windows デバイステストフレームワーク WDK、コンポーネント
- WDTF WDK、コンポーネント
- デバイス指向のターゲットオブジェクト WDK WDTF
- システム指向のターゲットオブジェクト WDK WDTF
- ターゲットオブジェクト WDK WDTF
- デバイスの引き取り用 WDK WDTF
- システム引き取りの WDK WDTF
- Simple Data 評価言語 WDK WDTF
- SDEL WDK WDTF
- コードモジュール WDK WDTF
- クエリ言語 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb616230159f4b975d6778dcb8c2521bf6840267
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844793"
---
# <a name="wdtf-architecture"></a>WDTF のアーキテクチャ


WDTF のアーキテクチャを理解するには、まず「 [Windows デバイステストフレームワークの設計ガイド」](wdtf-overview.md)を参照してください。 最も重要な概念は、WDTF がデバイスとシステムを使用することです。これは、それぞれを*ターゲット*( [**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)インターフェイス) に抽象化することによって行います。 次の図は、WDTF が提供するコアオブジェクトモデルを示しています。

![wdtf core オブジェクトモデルを示す図](images/wdtf-objectmodel.gif)

このシナリオでは、次の WDTF オブジェクトとインターフェイスの一部またはすべてを使用できます。

<a href="" id="wdtf-aggregation-object"></a>WDTF 集計オブジェクト  
WDTF aggregation オブジェクト ([**IWDTF2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)) は、フレームワーク全体の初期インスタンス化ポイントです。 フレームワーク内のすべての情報には、このオブジェクトを介してアクセスする必要があります。

<a href="" id="systemdepot-property"></a>[**Systemdepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_systemdepot)プロパティ  
[**Systemdepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_systemdepot)プロパティ ([**IWDTFSystemDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfsystemdepot2)) には、ローカルコンピューターのみが含まれています。この[**システム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfsystemdepot2-get_thissystem)プロパティを使用してアクセスできます。

<a href="" id="devicedepot-property"></a>[**Devicedepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_devicedepot)プロパティ  
[**Devicedepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_devicedepot)プロパティ ([**IWDTFDeviceDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfdevicedepot2)) は、コンピューターで使用可能なすべてのデバイスのコレクションを表します。 シナリオスクリプトでは、 [Simple Data 評価言語](simple-data-evaluation-language-overview.md)(sdel) を使用して、検索文字列で指定した1つ以上の条件を満たすデバイスの**devicedepot**プロパティを ([**クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query)メソッドで) 照会できます。 前の図に示されているように、**クエリ**は条件を満たすターゲット ([**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2)) のコレクションを返します。 さらに、 **Devicedepot**プロパティには[**rootdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfdevicedepot2-get_rootdevice)プロパティがあります。これは、コンピューターの物理的に存在する (*非ファントム*) デバイスの親である論理デバイスオブジェクトを表します。

<a href="" id="iwdtftarget2"></a>[**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)  
[**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)インターフェイスは、テストアクティビティの*ターゲット*を表します。 フレームワークで実行するすべてのアクティビティには、少なくとも1つのターゲットが含まれます。 ターゲットには、次のいずれかの形式を使用できます。

-   *デバイスの種類のターゲット*は、コンピューターに接続されているハードウェア (またはソフトウェア) デバイスを表します。

-   *システム型のターゲット*は、コンピューター全体を表します。

ターゲットには、デバイスまたはコンピューターを表す属性が含まれています。

<a href="" id="iwdtftargets2"></a>[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2)  
[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2) collection インターフェイスは、個々のターゲット ([**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)) のコレクションを表します。 [**IWDTFTargets2:: Query**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query)メソッドを使用すると、含まれているターゲットのサブセットを含む別のコレクションを取得できます。

### <a name="action-plug-ins"></a>アクションプラグイン

WDTF には、テストシナリオでターゲットを制御するために使用できる一連のインターフェイスと実装 ([**アクションインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)) が含まれています。 各実装は、有効または無効にしたり、i/o 操作を実行したりするなど、ターゲット固有のアクションを実行する方法を認識しています。 スクリプトでは、次の図に示すように、特定の実装を理解することなく、インターフェイス名を使用してこれらのインターフェイスを参照できます。

![target:: getinterface メソッドを示す図](images/wdtf-getinterface.gif)

これらのインターフェイスの詳細については、「[ターゲットの制御](controlling-targets.md)」を参照してください。

### <a name="simple-data-evaluation-language-sdel"></a>単純なデータ評価言語 (SDEL)

WDTF には、単純なクエリ言語、単純なデータ評価言語 (SDEL) が含まれています。これは XPath に似ており、属性または関係に基づいてターゲットを収集するタスクを簡略化します。 SDEL を使用すると、各ターゲットの属性とそれらの間のリレーションシップの両方に基づいて選択制約を定義する、簡単なクエリステートメントを作成できます。 SDEL の詳細については、「 [Simple Data 評価言語の概要](simple-data-evaluation-language-overview.md)」を参照してください。

 

 




