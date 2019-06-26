---
title: WDF のアーキテクチャ
description: WDF のアーキテクチャ
ms.assetid: e5e2ed4a-5faf-4879-965f-7316fe64edf9
keywords:
- カーネル モード ドライバー WDK KMDF、アーキテクチャ
- KMDF WDK、アーキテクチャ
- カーネル モード ドライバー フレームワーク WDK のアーキテクチャ
- WDK KMDF オブジェクトのメソッド
- WDK KMDF のアーキテクチャ
- オブジェクトの WDK KMDF イベント コールバック関数
- WDK KMDF のイベントのコールバック関数
- WDK KMDF オブジェクトのプロパティ
- オブジェクトは WDK KMDF を処理します。
- WDK KMDF インターフェイス
- オブジェクト WDK KMDF
- framework オブジェクト WDK KMDF、アーキテクチャ
- フレームワーク ベースのドライバー WDK KMDF、アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b907b9d17f971b79800f33cda68c4706c69748d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371103"
---
# <a name="wdf-architecture"></a>WDF のアーキテクチャ





WDF は、ドライバーのオブジェクト ベースのインターフェイスを提供します。 オブジェクトのフレームワークで定義されたインターフェイスが構成されます。

<a href="" id="object-methods"></a>*オブジェクトのメソッド*  
メソッドは、オブジェクトの操作を実行するか、取得またはオブジェクトのプロパティを設定するドライバーを呼び出すことができる関数です。 メソッドの名前は **Wdf * * * ObjectAction*ここで、*オブジェクト*オブジェクトの説明と*アクション*関数の動作を示します。 たとえば、 [ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)デバイス オブジェクトを作成します。

<a href="" id="object-event-callback-functions"></a>*オブジェクト イベントのコールバック関数*  
イベントのコールバック関数は、ドライバーを提供する関数です。 各イベントのコールバック関数は、オブジェクトで発生する特定のイベントに関連付けられます。 フレームワークは、関連付けられているイベントの発生時に、イベントのコールバック関数を呼び出します。 規則により、イベントのコールバック関数のプレース ホルダーと呼ばれます Evt*ObjectEvent*、できる任意の名前をこれらのコールバックは、ドライバーを選択します。 たとえば、ドライバーの登録、 [ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)そのデバイスが稼働状態になるときに通知するイベントのコールバック。

<a href="" id="object-properties"></a>*オブジェクトのプロパティ*  
プロパティは、値オブジェクト内に格納されていること、およびドライバー*取得*(つまり、取得) と*設定*(つまり、変更)。 多くの場合、プロパティは、対応する WDM オブジェクト内のフィールドに直接マップされます。 という名前のプロパティが失敗することはできません **Wdf***オブジェクト***取得 * * * 値*と **Wdf***オブジェクト***設定 * * * 値*、および失敗が許容されるプロパティ名前は **Wdf***オブジェクト***取得 * * * 値*と **Wdf***オブジェクト***割り当てる * * * 値*します。 *オブジェクト*、オブジェクトの説明と*値*関数を設定または取得するデータを識別します。 たとえば、 [ **WdfDeviceGetDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdriver)デバイス オブジェクトに関連付けられているドライバー オブジェクトへのハンドルを返します。

<a href="" id="object-handles"></a>*オブジェクト ハンドル*  
フレームワーク ベースのドライバーしない直接オブジェクトにアクセスするフレームワークです。 代わりに、ドライバーは、オブジェクトのメソッドに渡すことができるは、オブジェクト ハンドルを受け取ります。

フレームワークには、framework ベースのドライバーを使用するいくつかのオブジェクトの種類を定義します。

-   A *framework ドライバー オブジェクト*各ドライバーを表します。

-   A *framework デバイス オブジェクト*ドライバーがサポートする各デバイスを表します。

-   *フレームワークのキュー オブジェクト*デバイスの I/O 要求を受信するための I/O キューを表します。

-   *フレームワークの要求オブジェクト*I/O キューごとに受け取る I/O 要求を表します。

すべてのフレームワークを定義するオブジェクトの一覧は、次を参照してください。 [Framework オブジェクトの概要](summary-of-framework-objects.md)します。

 

 





