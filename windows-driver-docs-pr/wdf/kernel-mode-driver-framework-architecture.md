---
title: WDF のアーキテクチャ
description: WDF のアーキテクチャ
ms.assetid: e5e2ed4a-5faf-4879-965f-7316fe64edf9
keywords:
- カーネルモードドライバー WDK KMDF、アーキテクチャ
- KMDF WDK、アーキテクチャ
- カーネルモードドライバーフレームワーク WDK、アーキテクチャ
- オブジェクトメソッド WDK KMDF
- アーキテクチャ WDK KMDF
- オブジェクトイベントコールバック関数 WDK KMDF
- イベントコールバック関数 WDK KMDF
- オブジェクトのプロパティ WDK KMDF
- オブジェクトが WDK KMDF を処理する
- インターフェイス WDK KMDF
- オブジェクト WDK KMDF
- フレームワークオブジェクト WDK KMDF、アーキテクチャ
- フレームワークベースのドライバー WDK KMDF, アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 254208903863cf29473dd72f118e06ba28bdf041
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843157"
---
# <a name="wdf-architecture"></a>WDF のアーキテクチャ





WDF には、ドライバー用のオブジェクトベースのインターフェイスが用意されています。 フレームワーク定義のオブジェクトインターフェイスは、次の要素で構成されます。

<a href="" id="object-methods"></a>*オブジェクトメソッド*  
メソッドは、ドライバーがオブジェクトに対して操作を実行したり、オブジェクトプロパティを取得または設定したりするために呼び出すことができる関数です。 メソッドには、**Wdf * * * ObjectAction*という名前が付けられます。ここで、 *object*はオブジェクトを表し、*アクション*は関数の動作を示します。 たとえば、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)はデバイスオブジェクトを作成します。

<a href="" id="object-event-callback-functions"></a>*オブジェクトイベントのコールバック関数*  
イベントコールバック関数は、ドライバーが提供する関数です。 各イベントコールバック関数は、オブジェクトで発生する可能性のある特定のイベントに関連付けられています。 フレームワークは、関連付けられたイベントが発生したときに、イベントコールバック関数を呼び出します。 規則により、イベントコールバック関数のプレースホルダーは、".Evt*Objectevent*" と呼ばれますが、これらのコールバックにはドライバーで任意の名前を指定できます。 たとえば、ドライバーは、デバイスが動作状態になったときに通知されるように、 [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)イベントコールバックを登録します。

<a href="" id="object-properties"></a>*オブジェクトのプロパティ*  
プロパティは、オブジェクト内に格納される値であり、ドライバーが*取得*(つまり、取得) して*設定*(つまり、変更) することができます。 多くの場合、プロパティは、対応する WDM オブジェクトのフィールドに直接マップされます。 失敗しないプロパティには、**Wdf***object***Get ** * * 値および **Wdf***オブジェクト***セット * ** * 値が指定され、失敗する可能性のあるプロパティには、**Wdf***オブジェクト***の取得 * ** * 値と **Wdf***オブジェクト***の割り当て * * * という名前が付けられます。値*。 *オブジェクトはオブジェクトについて*説明し、 *Value*は関数が設定または返すデータを識別します。 たとえば、 [**Wdfdevicegetdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdriver)は、デバイスオブジェクトに関連付けられている driver オブジェクトへのハンドルを返します。

<a href="" id="object-handles"></a>*オブジェクトハンドル*  
フレームワークベースのドライバーは、フレームワークオブジェクトに直接アクセスすることはありません。 代わりに、ドライバーはオブジェクトハンドルを受け取ります。このハンドルはオブジェクトのメソッドに渡すことができます。

フレームワークは、フレームワークベースのドライバーが使用するオブジェクトの種類をいくつか定義します。

-   *フレームワークドライバーオブジェクト*は、各ドライバーを表します。

-   *フレームワークデバイスオブジェクト*は、ドライバーがサポートする各デバイスを表します。

-   *フレームワークキューオブジェクト*は、デバイスの i/o 要求を受信する i/o キューを表します。

-   *フレームワーク要求オブジェクト*は、各 i/o キューによって受信される i/o 要求を表します。

フレームワークによって定義されるすべてのオブジェクトの一覧については、「[フレームワークオブジェクトの概要](summary-of-framework-objects.md)」を参照してください。

 

 





