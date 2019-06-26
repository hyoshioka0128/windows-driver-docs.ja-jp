---
title: KMDF ドライバー用の WMI の概要
description: KMDF ドライバー用の WMI の概要
ms.assetid: e919f6c9-a4c5-4972-91e7-f4fa609455fe
keywords:
- WMI の WDK KMDF
- フレームワーク ベースのドライバーの WMI の詳細について、WMI の WDK KMDF
- WDK KMDF のコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83c58c615e5f92e45460b70dadf0e0c2fbacd9a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371109"
---
# <a name="introduction-to-wmi-for-kmdf-drivers"></a>KMDF ドライバー用の WMI の概要


\[KMDF にのみ適用されます。\]

カーネル モード ドライバー フレームワークに情報を提供するドライバーをサポートしている[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-wmi) (WMI)。 このようなドライバーが呼び出されて*データ プロバイダーの WMI*データを提供するため、 *WMI クライアント*、WMI から情報を受信登録されているアプリケーションであります。

WMI データ プロバイダーのサポート*WMI データ ブロック*次の 1 つ以上を表すことができます。

-   *データ項目*ドライバーを送信または WMI クライアントから受信するデバイスに固有のデータを格納します。

-   *メソッド*(関数) ドライバーは、WMI クライアントに代わって実行します。

-   *イベント*ドライバーがデバイスに固有のイベントの通知を受信登録している WMI クライアントに送信します。

WMI データ ブロックは、として指定*WMI クラス*.mof ファイルにします。 各 WMI データ ブロックは、GUID によって識別されます。

すべてのドライバーでは、自分のデバイス クラスに対する WMI を定義する標準の WMI データ ブロックをサポートする必要があります。 これらの WMI データ ブロックが定義されている*Wmicore.mof*します。

ドライバーでは、.mof ファイルに定義する WMI データのブロックもサポートできます。 定義およびカスタマイズされた WMI データ ブロックを発行する方法については、次のセクションを参照してください。

-   [WMI データとイベント ブロックの MOF 構文](https://docs.microsoft.com/windows-hardware/drivers/kernel/mof-syntax-for-wmi-data-and-event-blocks)

-   [WMI データとイベント ブロックの設計](https://docs.microsoft.com/windows-hardware/drivers/kernel/designing-wmi-data-and-event-blocks)

-   [WMI スキーマの公開](https://docs.microsoft.com/windows-hardware/drivers/kernel/publishing-a-wmi-schema)

-   [WMI プロパティ シート](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-property-sheets)

### <a name="framework-wmi-objects-and-callback-functions"></a>Framework の WMI オブジェクトとコールバック関数

フレームワークは、ドライバーは、WMI データ プロバイダーを実装するために使用できる 2 つのオブジェクトを定義します。 *WMI プロバイダー オブジェクト*ドライバーを提供する WMI データ ブロックのスキーマを表します。 *WMI インスタンス オブジェクト*特定のプロバイダーに関連付けられているデータ ブロックのインスタンスを表します。 ドライバーは、これら 2 つのオブジェクトを定義する次のイベントのコールバック関数を実装することで、WMI クライアントと通信します。

<a href="" id="evtwmiproviderfunctioncontrol"></a>[*EvtWmiProviderFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)  
有効にし、WMI データの収集および WMI イベントの送信用のドライバーのサポートを無効にします。

<a href="" id="evtwmiinstancequeryinstance"></a>[*EvtWmiInstanceQueryInstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)  
WMI プロバイダーのインスタンスのデータを WMI クライアントに配信します。

<a href="" id="evtwmiinstancesetinstance-and-evtwmiinstancesetitem"></a>[*EvtWmiInstanceSetInstance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)と[ *EvtWmiInstanceSetItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)  
クライアントが指定した値に、ドライバーのデータ ブロック内の情報を設定します。

<a href="" id="evtwmiinstanceexecutemethod"></a>[*EvtWmiInstanceExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)  
クライアントの要求で、ドライバーによって提供されるメソッドを実行します。

### <a name="sample-drivers-that-implement-wmi"></a>WMI を実装しているサンプル ドライバー

FIREFLY、PCIDRV、およびトースター[サンプル ドライバー](sample-kmdf-drivers.md) WMI のデータ プロバイダーします。

 

 





