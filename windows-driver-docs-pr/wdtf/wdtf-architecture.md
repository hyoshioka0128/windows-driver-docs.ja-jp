---
title: WDTF のアーキテクチャ
description: WDTF のアーキテクチャ
ms.assetid: 8c110e97-6870-41f1-a4f3-4d44b2974c1a
keywords:
- Windows デバイスのテスト フレームワーク WDK、アーキテクチャ
- WDTF WDK、アーキテクチャ
- WDK WDTF のアーキテクチャ
- Windows デバイスのテスト フレームワーク WDK、コンポーネント
- WDTF WDK、コンポーネント
- デバイス指向のターゲット オブジェクト WDK WDTF
- システム指向のターゲット オブジェクト WDK WDTF
- ターゲット オブジェクト WDK WDTF
- デバイス depot WDK WDTF
- システム depot WDK WDTF
- 単純なデータ評価言語 WDK WDTF
- SDEL WDK WDTF
- コード モジュール WDK WDTF
- クエリ言語 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67598676c713cc5dfdad490e7c33b1ff2210962f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368031"
---
# <a name="wdtf-architecture"></a>WDTF のアーキテクチャ


WDTF のアーキテクチャを理解するには、まずお読みください[Windows デバイスのテスト フレームワークの設計ガイド](wdtf-overview.md)します。 WDTF がそれぞれに抽象化することによって、デバイスと、システムを使用することは、最も重要な概念、*ターゲット*(、 [ **IWDTFTarget2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2)インターフェイス)。 次の図は、WDTF を提供する主要なオブジェクト モデルを示します。

![wdtf の主要なオブジェクト モデルを示す図](images/wdtf-objectmodel.gif)

シナリオには、次の WDTF オブジェクトとインターフェイスの一部またはすべてを使用できます。

<a href="" id="wdtf-aggregation-object"></a>WDTF 集計オブジェクト  
WDTF 集計オブジェクト ([**IWDTF2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)) フレームワーク全体の最初のインスタンス化のポイントです。 フレームワーク内のすべては、このオブジェクトを通じてアクセスする必要があります。

<a href="" id="systemdepot-property"></a>[**SystemDepot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtf2-get_systemdepot)プロパティ  
[ **SystemDepot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtf2-get_systemdepot)プロパティ ([**IWDTFSystemDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtfsystemdepot2)) のみ、ローカル コンピューター、経由でアクセスできますが含まれています[**あれば**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfsystemdepot2-get_thissystem)プロパティ。

<a href="" id="devicedepot-property"></a>[**DeviceDepot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtf2-get_devicedepot)プロパティ  
[ **DeviceDepot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtf2-get_devicedepot)プロパティ ([**IWDTFDeviceDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtfdevicedepot2)) コンピューターで使用できるすべてのデバイスのコレクションを表します。 シナリオのスクリプトを照会できます (で、 [**クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-query)メソッド)、 **DeviceDepot**を使用して、検索文字列で指定した 1 つまたは複数の条件を満たすデバイスのプロパティ[単純なデータ評価言語](simple-data-evaluation-language-overview.md)(SDEL)。 前の図に示すように**クエリ**ターゲットのコレクションを返します ([**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftargets2)) 条件に一致します。 さらに、 **DeviceDepot**プロパティは、 [ **RootDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfdevicedepot2-get_rootdevice) (も存在する物理的にすべての親である論理デバイス オブジェクトを表すプロパティ呼ばれる*非ファントム*)、コンピューターのデバイス。

<a href="" id="iwdtftarget2"></a>[**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2)  
[ **IWDTFTarget2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2)インターフェイスが表現を*ターゲット*のアクティビティをテストします。 フレームワークを使用して実行するすべてのアクティビティには、少なくとも 1 つのターゲットが含まれます。 ターゲットは、次の形式のいずれかを設定できます。

-   A*デバイスの種類のターゲット*コンピューターに接続されているハードウェア (またはソフトウェア) デバイスを表します。

-   A*システム型のターゲット*全体のコンピューターを表します。

ターゲットには、デバイスやコンピューターを表す方法を説明する属性が含まれています。

<a href="" id="iwdtftargets2"></a>[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftargets2)  
[ **IWDTFTargets2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftargets2)コレクション インターフェイスは、個々 のターゲットのコレクションを表します ([**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2))。 [ **IWDTFTargets2::Query** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-query)メソッドでは、含まれているターゲットのサブセットを含む別のコレクションを取得することができます。

### <a name="action-plug-ins"></a>操作プラグイン

WDTF には一連インターフェイスと実装にはが含まれています ([**アクション インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)) コントロール ターゲットに、テストのシナリオで使用することができます。 各実装は、有効化し無効化、または I/O 操作を実行するなどのターゲット固有のアクションを実行する方法を認識します。 スクリプトは、次の図のように、特定の実装を理解することがなく、インターフェイス名でこれらのインターフェイスを参照できます。

![target::getinterface メソッドを示す図](images/wdtf-getinterface.gif)

これらのインターフェイスの詳細については、次を参照してください。[を制御するターゲット](controlling-targets.md)します。

### <a name="simple-data-evaluation-language-sdel"></a>単純なデータ評価言語 (SDEL)

WDTF には、単純なクエリ言語では、単純なデータ評価言語 (SDEL)、XPath と同様、属性またはリレーションシップに基づくターゲットを収集する場合のタスクを簡素化が含まれています。 SDEL では、各ターゲットとそれらの間のリレーションシップの両方の属性に基づく選択範囲の制約を定義するフォームの簡単なクエリ ステートメントにできます。 SDEL の詳細については、次を参照してください。[単純なデータ評価言語の概要](simple-data-evaluation-language-overview.md)します。

 

 




