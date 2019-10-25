---
title: センサー ドライバーのイベントについて
description: センサー ドライバーのイベントについて
ms.assetid: 1e747743-f701-4854-92be-7b55c39fee08
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f6884756957e2ff96e6a51c85617457710e464ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824295"
---
# <a name="about-sensor-driver-events"></a>センサー ドライバーのイベントについて


アプリケーションでセンサーから情報を取得するには、センサードライバーによって発生するイベントをサブスクライブすることによって、同期的に、特定のプロパティまたはデータフィールドを要求する、または非同期的に行うという2つの方法があります。

センサードライバーは、**状態変更イベント**を発生させることができます。これは、デバイスでの移行についての通知をアプリケーションに通知し、その他の種類のイベント通知を実行します。 ドライバーは、デバイスが提供するセンサーごとに個別のイベントを発生させる必要があります。

**注**  [**Iwdfdevice::P ostevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-postevent)を使用してセンサーイベントを発生させることはできません。 センサープラットフォームは、接続されたクライアントプログラムにこのようなイベントを転送しません。

 

## <a name="state-change-events"></a>状態変更イベント

センサードライバーは、センサークラス拡張の[**ISensorClassExtension::P oststatechange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)メソッドを呼び出すことによって、状態変更イベントを発生させます。 たとえば、センサーの初期化を完了したドライバーは、このメソッドを呼び出して、センサー\_STATE\_READY という名前の新しい[**Sensorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)値を通知します。

## <a name="event-constants"></a>イベント定数

センサープラットフォームは、ドライバーイベントの次の定数を定義します。

**センサーイベントの種類**

センサープラットフォームでは、次のセンサーイベントの種類の識別子が定義されています。

| 名前 | 説明 |
| --- | --- |
| SENSOR_EVENT_DATA_UPDATED | 新しいデータが使用可能であることを示します。
| SENSOR_EVENT_PROPERTY_CHANGED| プロパティ値が変更されたことを示します。|
| SENSOR_EVENT_STATE_CHANGED| SENSOR_STATE_INITIALIZING から SENSOR_STATE_READY など、操作状態が変更されたことを示します。|


**センサーイベントの PROPERTYKEYs**

センサープラットフォームは、センサーイベントのパラメーターを識別するために、次の**Propertykeys**を定義します。

| 名前 | 説明 |
| --- | --- |
| SENSOR_EVENT_PARAMETER_EVENT_ID| IPortableDeviceValues の GUID 値が、SENSOR_EVENT_DATA_UPDATED などのイベントの種類の ID であることを示します。|
| SENSOR_EVENT_PARAMETER_STATE| IPortableDeviceValues の符号なし整数値がセンサーの状態 (SENSOR_STATE_READY など) であることを示します。<br>**メモ**状態変更イベントを発生させるには、 [ISensorClass Extension::P oststatechange](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)を呼び出します。 SENSOR_EVENT_PARAMETER_STATE を明示的に指定しなくてもイベントを発生させることができます。|

## <a name="other-events"></a>その他のイベント

センサードライバーは、センサークラス拡張の[**ISensorClassExtension::P ostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)メソッドを呼び出すことによって、他のすべての種類のイベントを発生させます。 このメソッドは、動作状態に関係のないセンサーイベントを生成するための、汎用的な拡張可能な方法を提供します。 **Postevent**への各呼び出しには、 [Iportabledevicevaluescollection](https://go.microsoft.com/fwlink/p/?linkid=131487)へのポインターが含まれています。 このコレクション内の各[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)オブジェクトには、センサー\_イベント\_パラメーター\_イベントの種類を識別するイベント\_ID プロパティの**GUID**値、およびオプションのデータフィールド値が含まれています。イベントデータを格納します。 たとえば、新しい都市データを含む GPS ドライバーでは、センサー\_イベント\_データ\_更新されたイベント ID を使用し、センサー\_データ\_CITY プロパティキーの文字列値を指定します。

ドライバーによってイベントがポストされると、センサークラスの拡張機能によって、イベントとそれに関連付けられているすべてのデータがセンサー API に転送されます。

プラットフォーム定義定数の定義は、"センサー. h" という名前のファイルにあります。 プラットフォーム定義センサー定数の詳細については、「[定数](about-sensor-constants.md)」を参照してください。

## <a name="managing-sensor-driver-events"></a>センサードライバーイベントの管理

ドライバーがイベント要求を受け入れる前に、イベントを生成してポストするための別のスレッドを作成する必要があります。 スレッドを使用すると、データ要求のコールバックなどの同期プロシージャを頻繁に発生させないようにすることができます。 データ更新イベントを発生させるスレッドクラスの例については、「[データ更新イベントの発生](raising-events.md)」を参照してください。

少なくとも1つのクライアントアプリケーションがイベント通知を要求している場合にのみ、センサーでイベントを発生させる必要があります。 アプリケーションが状態変更イベントなどのイベント通知を要求すると、センサークラスの拡張機能は[**ISensorDriver:: OnClientSubscribeToEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)を使用してドライバーに通知します。 このメソッドは、アプリケーションを識別する[Iwdffile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)ポインターと、アプリケーションがイベント通知を要求しているセンサーを識別する文字列を提供します。 IWDFFile ポインターを一意の識別子として使用すると、イベントにサブスクライブしているアプリケーションを追跡できます。 センサーは特定のクライアント向けのイベントを発生させることはできませんが、センサー\_プロパティ\_現在の\_レポート\_間隔などの特定のプロパティの値を設定することが必要になる場合もあります。センサー\_プロパティ\_\_の感度を変更します。

たとえば、複数のクライアントアプリケーションでセンサー\_プロパティに異なる値が設定されている場合\_現在の\_レポート\_間隔では、イベントの頻度を、要求された最短の間隔に設定するルールを適用できます。 ただし、新しいクライアントがイベントまたは既存のクライアントアンサブスクライブにサブスクライブするたびに、センサーで間隔を調整することが必要になる場合があります。 コード例を含むレポート間隔の詳細については、「[データのフィルター選択](filtering-data.md)」を参照してください。

### <a name="sensor-events-and-data-privacy"></a>センサーイベントとデータのプライバシー

他のデータ要求と同様に、イベント通知の要求はセンサークラス拡張を使用してセキュリティで保護されます。 クラス拡張では、このデータを要求するユーザーに対してのみ位置データが許可されます。

>[!CAUTION]
> センサーのすべての i/o 要求を処理するためにセンサークラス拡張を使用するようにしてください。 これにより、ユーザーの個人情報が漏洩する可能性は低くなります。

 

データのプライバシーの詳細については、「[センサーと場所のプラットフォームのプライバシーとセキュリティ](https://docs.microsoft.com/windows-hardware/drivers/gnss/privacy-and-security-in-the-sensor-and-location-platform)」を参照してください。

## <a name="related-topics"></a>関連トピック
[**センサーのプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-properties)



