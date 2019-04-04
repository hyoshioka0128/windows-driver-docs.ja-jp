---
title: センサー ドライバーのイベントについて
description: センサー ドライバーのイベントについて
ms.assetid: 1e747743-f701-4854-92be-7b55c39fee08
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e8a832ca852e627707af3ccc03b4ee285dcd1613
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531579"
---
# <a name="about-sensor-driver-events"></a>センサー ドライバーのイベントについて


アプリケーションは、2 つの方法でのセンサーから情報を受け取ることができます。 特定のプロパティまたはフィールドのデータを要求することによって同期的に、またはセンサー ドライバーで発生するイベントをサブスクライブして、非同期的にします。

発生する可能性がセンサー ドライバー**状態変更イベント**、新しいオペレーションの条件とその他のイベント通知をデバイスでの遷移をアプリケーションに通知します。 ドライバーは、デバイスを提供する各センサーの個別のイベントを発生させる必要があります。

**注**  使用しないでください[ **IWDFDevice::PostEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff558835)センサー イベントを発生させます。 センサー プラットフォームは、接続されているクライアントのプログラム には、このようなイベントを転送しません。

 

## <a name="state-change-events"></a>状態変更イベント

センサー ドライバーは、センサー クラスの拡張を呼び出して、状態変更イベントを発生させる[ **ISensorClassExtension::PostStateChange** ](https://msdn.microsoft.com/library/windows/hardware/ff545523)メソッド。 たとえば、センサーの初期化が終了するドライバーが、新しい通知するには、このメソッドを呼び出す[ **SensorState** ](https://msdn.microsoft.com/library/windows/hardware/ff545708)センサーをという名前の値\_状態\_準備。

## <a name="event-constants"></a>イベント定数

センサー プラットフォームでは、ドライバーのイベントの次の定数を定義します。

**センサー イベントの種類**

センサー プラットフォームでは、次のセンサー イベントの種類の識別子を定義します。

| 名前 | 説明 |
| --- | --- |
| SENSOR_EVENT_DATA_UPDATED | 新しいデータが使用できることを示します。
| SENSOR_EVENT_PROPERTY_CHANGED| プロパティ値が変更されたことを示します。|
| SENSOR_EVENT_STATE_CHANGED| たとえば、操作の状態の変更を SENSOR_STATE_READY SENSOR_STATE_INITIALIZING からを示します。|


**センサー イベント PROPERTYKEYs**

センサー プラットフォームは、次を定義します。 **PROPERTYKEYs**センサー イベントのパラメーターを特定します。

| 名前 | 説明 |
| --- | --- |
| SENSOR_EVENT_PARAMETER_EVENT_ID| IPortableDeviceValues で GUID の値が SENSOR_EVENT_DATA_UPDATED など、イベントの種類 ID であることを示します。|
| SENSOR_EVENT_PARAMETER_STATE| IPortableDeviceValues の符号なし整数値が SENSOR_STATE_READY など、センサーの状態であることを示します。<br>**注**状態変更イベントを発生させるのには、呼び出す[ISensorClass Extension::PostStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)します。 イベントを発生させる SENSOR_EVENT_PARAMETER_STATE を明示的に指定する必要はありません。|

## <a name="other-events"></a>その他のイベント

センサー ドライバーは、センサー クラスの拡張を呼び出して、その他のすべての種類のイベントを発生させる[ **ISensorClassExtension::PostEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)メソッド。 このメソッドは、ジェネリック、拡張可能な稼動状態に関係のないセンサー イベントを発生させる方法を提供します。 呼び出しごとに**PostEvent**へのポインターを含む[IPortableDeviceValuesCollection](https://go.microsoft.com/fwlink/p/?linkid=131487)します。 各[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)このコレクション内のオブジェクトが含まれています、 **GUID**センサー値\_イベント\_パラメーター\_イベント\_IDイベントの種類を識別するプロパティとイベント データを含む省略可能なデータ フィールドの値。 たとえば、新しい都市のデータを持つ GPS ドライバーは、センサーを使用して\_イベント\_データ\_イベント ID を更新し、センサーの文字列値を指定\_データ\_型\_CITY プロパティのキー。

後は、ドライバーは、イベントを投稿記事、センサー クラスの拡張機能は、イベントと関連データをセンサー API に転送します。

Sensors.h という名前のファイルのプラットフォームで定義されている定数の定義が表示されます。 センサーのプラットフォームで定義されている定数の詳細については、[定数](about-sensor-constants.md)を参照してください。

## <a name="managing-sensor-driver-events"></a>センサー ドライバーのイベントの管理

イベントの要求を受け入れると、ドライバー、前に別のスレッドを生成し、イベントを投稿を作成する必要があります。 スレッドを使用すると、頻繁にイベント プロシージャがデータ要求のコールバックなどの同期プロシージャをブロックするを防ぐことできます。 データ更新イベントを発生させるスレッド クラスの例は、[Raising Data-Updated イベント](raising-events.md)を参照してください。

センサーは、少なくとも 1 つのクライアント アプリケーションには、イベント通知が要求した場合にのみ、イベントを発生させる必要があります。 センサー クラスの拡張機能を使ってドライバーに通知、アプリケーションの状態変更イベントを含む、イベント通知を要求すると[ **ISensorDriver::OnClientSubscribeToEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)します。 この方法では、 [IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)アプリケーションおよびアプリケーションがイベント通知を要求するセンサーを識別する文字列を識別するポインター。 一意の識別子として IWDFFile ポインターを使用して、イベントにサブスクライブしているアプリケーションの追跡に役立つことができます。 特定のセンサーなどのプロパティの値がどのアプリケーション セットを追跡する必要がありますが、センサーは、特定のクライアントに送信されるイベントを発生させることはできません、\_プロパティ\_現在\_レポート\_間隔またはセンサー\_プロパティ\_変更\_と小文字の区別します。

たとえば、複数のクライアント アプリケーションは、センサーの異なる値を設定\_プロパティ\_現在\_レポート\_間隔が最短の間隔にイベントの頻度を設定する規則を適用できます要求されています。 ただし、センサーが毎回の間隔を調整する必要があります、新しいクライアントがイベントをサブスクライブまたは既存のクライアントをアンサブスク ライブします。 コードの例を含む、レポート間隔の詳細については、[データのフィルター処理](filtering-data.md)を参照してください。

### <a name="sensor-events-and-data-privacy"></a>センサーのイベントとデータのプライバシー

その他のデータ要求のようにイベント通知の要求は、センサー クラスの拡張機能を使用してセキュリティで保護された行われます。 クラスの拡張機能では、このデータを要求するユーザーに対してのみ場所データができます。

>[!CAUTION]
> センサー クラスの拡張機能を使用して、センサーのすべての I/O 要求を処理することを確認してください。 これにより、ユーザーの個人情報を表示する可能性を低減しています。

 

データのプライバシーの詳細については、次を参照してください[Sensor and Location プラットフォーム セキュリティとプライバシー。](https://docs.microsoft.com/windows-hardware/drivers/gnss/privacy-and-security-in-the-sensor-and-location-platform)

## <a name="related-topics"></a>関連トピック
[**センサーのプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-properties)



