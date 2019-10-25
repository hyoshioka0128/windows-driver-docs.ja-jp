---
title: ドライバーでの WMI のデータ ブロックとイベントのサポート
description: ドライバーでの WMI のデータ ブロックとイベントのサポート
ms.assetid: a5138413-3ec4-4c61-9f00-6604759532e9
keywords:
- WMI WDK KMDF、データブロック
- WMI WDK KMDF、イベント
- WMI データブロックの読み取り/書き込み (WDK KMDF)
- 読み取り専用 WMI データブロック WDK KMDF
- イベント WDK KMDF、WMI
- WDK KMDF のトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb2c26586dcec4ff04ac83fb49b7b78c48a54122
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831678"
---
# <a name="supporting-wmi-data-blocks-and-events-in-your-driver"></a>ドライバーでの WMI のデータ ブロックとイベントのサポート


\[は KMDF にのみ適用され\]

フレームワークベースのドライバーは、イベントコールバック関数を提供することによって、WMI データブロックをサポートします。 ドライバーは、WMI クライアントにイベントを送信するオブジェクトメソッドを呼び出すことによって、WMI イベントをサポートします。

### <a href="" id="supporting-read-write-wmi-data-blocks"></a>読み取り/書き込み WMI データブロックのサポート

Wmi データブロック内の情報が、WMI クライアントによって読み取りと書き込みが可能である場合、ドライバーは、クライアントの読み取り要求と[*Evtwmiinstancequeryinstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)を処理する[*Evtwmiinstancequeryinstance コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)[*関数を提供する必要があります。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)クライアントの書き込み要求を処理する EvtWmiInstanceSetItem コールバック関数 (またはその両方)。

ドライバーがクライアントの要求で実行するメソッドがデータブロックに含まれている場合、ドライバーは[*Evtwmiinstanceexecutemethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)コールバック関数も提供する必要があります。

WMI データブロックが書き込み専用の場合 (つまり、WMI クライアントがデータブロックに情報を書き込むことができても、データブロックを読み取ることができない場合)、ドライバーは[*Evtwmiinstancequeryinstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)コールバック関数を提供しません。

### <a href="" id="supporting-read-only-wmi-data-blocks"></a>読み取り専用の WMI データブロックのサポート

Wmi データブロック内の情報を WMI クライアントで変更できない場合、ドライバーは[*Evtwmiinstancesetinstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)または[*EvtWmiInstanceSetItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item) callback 関数を提供しません。 WMI クライアントからのデータブロック情報の要求をサポートするために、ドライバーは次のいずれかを実行できます。

-   ドライバーが提供するデータを WMI によって提供されるバッファーにコピーするために、 [*Evtwmiinstancequeryinstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)コールバック関数を指定します。

-   データブロックの情報を WMI インスタンスオブジェクトの[コンテキスト空間](framework-object-context-space.md)に格納し、インスタンスの[**WDF\_WMI\_\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config)の**UseContextForQuery**メンバーを**TRUE**に設定します。

ドライバーで**UseContextForQuery**が**TRUE**に設定されている場合、wmi クライアントがインスタンスの情報を要求すると、インスタンスオブジェクトのコンテキスト空間が wmi によって指定されたバッファーにコピーされます。 ドライバーに、オブジェクトコンテキスト領域からの読み取り専用の固定長データを提供する単一の WMI インスタンスしかない場合、 *EvtWmiInstanceXxx*コールバックは必要ありません。

読み取り専用のデータブロックに、ドライバーがクライアントの要求で実行するメソッドが含まれている場合、ドライバーは[*Evtwmiinstanceexecutemethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)コールバック関数を提供することもできます。

### <a name="supporting-expensive-wmi-data-blocks"></a>高価な WMI データブロックのサポート

ドライバーが WMI データブロックの1つをサポートするために比較的大量の動的データを収集する場合、ドライバーは次の操作を実行する必要があります。

-   WMI プロバイダーオブジェクトの[**WDF\_wmi\_provider\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)構造体の**Flags**メンバーに**WdfWmiProviderExpensive**フラグを設定して、データブロックを "高額" に宣言します。

-   データブロックのデータ収集を有効または無効にする[*Evtwmiproviderfunctioncontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)コールバック関数を指定するか、 [**WdfWmiProviderIsEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiproviderisenabled)を呼び出して、ドライバーでデータ収集を有効にするか無効にするかを決定します。

ドライバーで**WdfWmiProviderExpensive**フラグが設定されている場合、フレームワークは、WMI クライアントがデータブロックにアクセスするために登録するときに、 [*Evtwmiproviderfunctioncontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)コールバック関数を呼び出します。 コールバック関数では、ドライバーがデータを収集する機能を有効にする必要があります。 すべての WMI クライアントがデータブロックの登録を削除した場合、フレームワークは*Evtwmiproviderfunctioncontrol*コールバック関数を再度呼び出して、ドライバーがデータの収集を停止できるようにします。

### <a name="supporting-wmi-events"></a>WMI イベントのサポート

ドライバーは WMI イベントを使用して、WMI クライアントに例外条件を通知することができます。 (エラーをログに記録する代わりに、WMI イベントを使用しないでください)。データ項目と同様に、WMI イベントは、マネージオブジェクト形式 (.mof) ファイル内の WMI データブロックで定義されます。

Wmi クライアントは、WMI イベントの通知を登録します。 登録されている WMI クライアントにイベントを送信するために、ドライバーは[**WdfWmiInstanceFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancefireevent)メソッドを呼び出します。 このメソッドを使用すると、ドライバーは必要に応じて、イベント固有のデータをクライアントに送信できます。

イベントを定義する WMI データブロックにも WMI データ項目またはメソッド項目が含まれている場合、ドライバーは適切な WMI コールバック関数を提供します。 データブロックにイベントが定義されていても、データやメソッドの項目が含まれていない場合、ドライバーは wmi プロバイダーオブジェクトの[**WDF\_wmi\_provider\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)の**Flags**メンバーにある**WdfWmiProviderEventOnly**フラグを設定する必要があります。データ.

WMI クライアントがイベント通知用に登録されている場合にのみ、ドライバーは[**WdfWmiInstanceFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancefireevent)を呼び出す必要があります。 ドライバーは、 [*Evtwmiproviderfunctioncontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)コールバック関数を指定するか、 [**WdfWmiProviderIsEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiproviderisenabled)を呼び出すことによって、 **WdfWmiInstanceFireEvent**を呼び出す必要があるかどうかを判断できます。

### <a name="supporting-wmi-event-tracing"></a>サポート (WMI イベントトレースを)

トレースイベントは、他の WMI イベントと同じ方法で、.mof ファイルで定義されます。 ドライバーがトレースイベントの WMI プロバイダーオブジェクトを作成するときは、プロバイダーオブジェクトの[**WDF\_wmi\_provider\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)構造体の**Flags**メンバーで、 **WdfWmiProviderTracing**フラグを設定する必要があります。

プロバイダーインスタンスが登録されると、ドライバーは[**WdfWmiProviderGetTracingHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiprovidergettracinghandle)を呼び出してトレースハンドルを取得できます。 ドライバーは、 [**WmiTraceMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessage)ルーチンへの入力としてトレースハンドルを使用できます。

イベントトレースの詳細については、以下を参照してください。

-   [WMI イベントのトレース](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)

-   [WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

 

 





