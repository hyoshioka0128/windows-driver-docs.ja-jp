---
title: ISensorDriver について
description: ISensorDriver について
ms.assetid: 2c51c235-e402-4f89-bff5-39af87d95e19
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4ed91254e87d440d54bfe110540c8c706d1cb1f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842457"
---
# <a name="about-isensordriver"></a>ISensorDriver について


センサードライバーは、 [ISensorDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nn-sensorsclassextension-isensordriver)インターフェイスを実装する必要があります。 このインターフェイスを使用すると、ドライバーは、センサーがサポートするセンサーの種類、プロパティ、データフィールド、イベント、および実際のプロパティ値とセンサーデータに関する情報を提供します。 クラス拡張は、コールバックメソッドを呼び出して、i/o 要求を処理し、API レイヤーが要求するプロパティの一覧を指定して、クライアント接続を管理し、イベントをサブスクライブします。

## <a name="method-to-enumerate-sensors"></a>センサーを列挙する方法

クラス拡張は、常に[**ISensorDriver:: OnGetSupportedSensorObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)を呼び出すことによって、デバイスで使用可能なセンサーを列挙します。 各センサーについて、ドライバーは、(デバイスに固有の) 文字列 ID とその他の必要なプロパティ値を含む[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)オブジェクトを返す必要があります。

## <a name="methods-to-manage-client-connections"></a>クライアント接続を管理する方法

接続と切断を行うクライアントアプリケーションについてドライバーに通知するために、センサークラス拡張は[**ISensorDriver:: OnClientConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientconnect)と[**ISensorDriver:: onclientconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientdisconnect)を呼び出します。 これらのコールバックメソッドは、 [Iwdffile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)インターフェイスへのポインターとセンサー ID の2つのパラメーターを渡します。 ドライバーは、各クライアントアプリケーションを表す一意の ID として、このインターフェイスポインターを使用する必要があります。 センサー ID には、クライアントが接続または切断するセンサーを識別する文字列が含まれています。 これらの値は、センサーの設定を管理できるように、クライアントとその接続先のセンサーの一覧を保持する必要がある場合に便利です。 たとえば、複数のクライアントからの競合する値が指定されている場合に、現在のレポート間隔を設定する方法をヒューリスティックにすることができます。 また、この情報を使用して、電源管理に関する意思決定を行うこともできます。 たとえば、クライアントが接続されていない場合は、センサーハードウェアを省電力モードにすることができます。

## <a name="methods-to-manage-event-subscribers"></a>イベントサブスクライバーを管理する方法

センサークラス拡張は、クライアントアプリケーションがイベントを管理するのに役立つメソッドを呼び出します。 [**ISensorDriver:: OnGetSupportedEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)は、ドライバーが発生させることができるイベントの一覧を取得します。 [**ISensorDriver:: OnClientSubscribeToEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)と[**ISensorDriver:: OnClientUnsubscribeFromEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents)は、特定のアプリケーションがイベント通知の受信またはキャンセルを要求したときに、ドライバーへの通知を提供します。 イベントをサブスクライブまたはサブスクライブ解除できるのは、接続されているクライアントだけです。

## <a name="methods-to-manage-data-and-properties"></a>データとプロパティを管理する方法

クライアントアプリケーションは、センサーデータを**データフィールド**として取得したり、センサーデバイスに関するメタデータを含む**プロパティ**を取得したりすることもできます。 サポートされているデータフィールドまたはプロパティの一覧を取得するために、センサークラス拡張は[**ISensorDriver:: OnGetSupportedDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields)または[**ISensorDriver:: OnGetSupportedProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties)を呼び出します。 データフィールドまたはプロパティ値を取得するために、クラス拡張は[**ISensorDriver:: OnGetDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields)または[**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)を呼び出します。 設定できるプロパティの場合、クラス拡張は[**ISensorDriver:: OnSetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onsetproperties)を呼び出して、新しいプロパティ値を提供します。

## <a name="methods-to-manage-wpd-commands"></a>WPD コマンドを管理する方法

センサークラスの拡張機能が、ハンドラーを提供していない[**ISensorClassExtension::P rocessiocontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol)を介して i/o 制御コマンドを受信した場合は、 [**ISensorDriver:: OnProcessWpdMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onprocesswpdmessage)を呼び出します。 このコールバックメソッドは、WPD コマンドが処理されていないことをドライバーに通知し、ドライバーにコマンドを処理する機会を与えます。 これは、センサープラットフォームの機能を拡張するために、カスタムの WPD コマンドを作成し、ドライバーにカスタムハンドラーを提供できることを意味します。

 

 




