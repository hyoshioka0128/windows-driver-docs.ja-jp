---
title: KMDF ドライバー用の WMI の概要
description: KMDF ドライバー用の WMI の概要
ms.assetid: e919f6c9-a4c5-4972-91e7-f4fa609455fe
keywords:
- WMI WDK KMDF
- WMI WDK KMDF、フレームワークベースのドライバーの WMI について
- コールバック関数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 460e1ae7255bf253fb881d3fe434aa8c6fa0e428
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843159"
---
# <a name="introduction-to-wmi-for-kmdf-drivers"></a>KMDF ドライバー用の WMI の概要


\[は KMDF にのみ適用され\]

カーネルモードドライバーフレームワークでは、 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-wmi) (WMI) に情報を提供するドライバーがサポートされています。 このようなドライバーは、wmi から情報を受信するように登録されているアプリケーションである wmi*クライアント*にデータを提供するため、 *wmi データプロバイダー*と呼ばれます。

WMI データプロバイダーは、次の1つまたは複数を表す*wmi データブロック*をサポートしています。

-   *データ項目*。ドライバーが WMI クライアントとの間で送受信するデバイス固有のデータを格納します。

-   WMI クライアントの代わりにドライバーが実行する*メソッド*(functions)。

-   デバイス固有のイベントの通知を受信するように登録されている WMI クライアントにドライバーが送信する*イベント*。

WMI データブロックは、.mof ファイルで*wmi クラス*として指定されます。 各 WMI データブロックは GUID によって識別されます。

すべてのドライバーは、WMI がデバイスクラスに対して定義する標準の WMI データブロックをサポートしている必要があります。 これらの WMI データブロックは、 *Wmicore*で定義されています。

また、ドライバーでは、.mof ファイルで定義した WMI データブロックをサポートすることもできます。 カスタマイズした WMI データブロックを定義して公開する方法については、次のセクションを参照してください。

-   [WMI データとイベントブロックの MOF 構文](https://docs.microsoft.com/windows-hardware/drivers/kernel/mof-syntax-for-wmi-data-and-event-blocks)

-   [WMI データとイベントブロックのデザイン](https://docs.microsoft.com/windows-hardware/drivers/kernel/designing-wmi-data-and-event-blocks)

-   [WMI スキーマの公開](https://docs.microsoft.com/windows-hardware/drivers/kernel/publishing-a-wmi-schema)

-   [WMI プロパティシート](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-property-sheets)

### <a name="framework-wmi-objects-and-callback-functions"></a>フレームワーク WMI オブジェクトとコールバック関数

このフレームワークでは、ドライバーが WMI データプロバイダーを実装するために使用できる2つのオブジェクトが定義されています。 *Wmi プロバイダーオブジェクト*は、ドライバーが提供する wmi データブロックのスキーマを表します。 *WMI インスタンスオブジェクト*は、特定のプロバイダーに関連付けられているデータブロックのインスタンスを表します。 ドライバーは、これら2つのオブジェクトが定義する次のイベントコールバック関数を実装することで、WMI クライアントと通信します。

<a href="" id="evtwmiproviderfunctioncontrol"></a>[*EvtWmiProviderFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)  
WMI データを収集し、WMI イベントを送信するドライバーのサポートを有効または無効にします。

<a href="" id="evtwmiinstancequeryinstance"></a>[*EvtWmiInstanceQueryInstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)  
Wmi プロバイダーのインスタンスデータを WMI クライアントに配信します。

<a href="" id="evtwmiinstancesetinstance-and-evtwmiinstancesetitem"></a>[*Evtwmiinstancesetinstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)と[ *EvtWmiInstanceSetItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)  
ドライバーのデータブロックの情報を、クライアントが指定した値に設定します。

<a href="" id="evtwmiinstanceexecutemethod"></a>[*EvtWmiInstanceExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)  
クライアントの要求で、ドライバーによって提供されるメソッドを実行します。

### <a name="sample-drivers-that-implement-wmi"></a>WMI を実装するサンプルドライバー

FIREFLY PCIDRV、およびトースター[サンプルドライバー](sample-kmdf-drivers.md)は、WMI データプロバイダーです。

 

 





