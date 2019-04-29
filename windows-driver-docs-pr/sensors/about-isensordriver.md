---
title: ISensorDriver について
description: ISensorDriver について
ms.assetid: 2c51c235-e402-4f89-bff5-39af87d95e19
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0e56cb8067e009a760f6f6edaf87836d03fa3d9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325970"
---
# <a name="about-isensordriver"></a>ISensorDriver について


センサー ドライバーを実装する必要があります、 [ISensorDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nn-sensorsclassextension-isensordriver)インターフェイス。 このインターフェイスでは、ドライバーはどの種類のセンサー、プロパティ、データ フィールド、およびイベント、センサーをサポートするだけでなく実際のプロパティの値とセンサーのデータに関する情報を提供します。 クラスの拡張機能は、イベントをサブスクライブして、クライアント接続を管理する API レイヤー要求のプロパティの一覧を指定して、I/O 要求を処理するコールバック メソッドを呼び出します。

## <a name="method-to-enumerate-sensors"></a>センサーを列挙するメソッド

クラス拡張は呼び出すことによって、デバイスの使用可能なセンサーを列挙常に、まず[ **ISensorDriver::OnGetSupportedSensorObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)します。 各のセンサーには、ドライバーを返す必要があります、 [IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)文字列 ID (デバイスの一意の) およびその他を含むオブジェクトには、プロパティの値が必要です。

## <a name="methods-to-manage-client-connections"></a>クライアント接続を管理する方法

接続、切断、センサー クラスの拡張機能をクライアント アプリケーションについて、ドライバーに通知する呼び出し[ **ISensorDriver::OnClientConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientconnect)と[ **ISensorDriver::OnClientDisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientdisconnect)します。 これらのコールバック メソッドが 2 つのパラメーターを渡す: へのポインター、 [IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)インターフェイスとセンサーの id。 ドライバーは、各クライアント アプリケーションを表す一意の ID としてこのインターフェイス ポインターを使用する必要があります。 センサー ID には、センサーを接続または切断する必要があるクライアントを識別する文字列が含まれています。 これらの値は、クライアントとセンサーがセンサーの設定を管理できるようにを接続の一覧を管理するために便利です。 たとえば、複数のクライアントから競合する値が指定されると、現在のレポート間隔を設定する方法についてのヒューリスティックがあります。 電源管理に関する意思決定にこの情報を使用することもできます。 たとえば、クライアントが接続されていない場合は、省電力モードにセンサー ハードウェアを配置できます。

## <a name="methods-to-manage-event-subscribers"></a>イベント サブスクライバーを管理する方法

センサー クラスの拡張機能は、クライアント アプリケーションがイベントを管理するメソッドを呼び出します。 [**ISensorDriver::OnGetSupportedEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)ドライバーを発生させるイベントの一覧を取得します。 [**ISensorDriver::OnClientSubscribeToEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)と[ **ISensorDriver::OnClientUnsubscribeFromEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents)に通知するときに、特定のドライバーアプリケーションは、受信、またはイベント通知のキャンセルを要求しました。 接続されているクライアントだけでは、購読したり、イベント サブスクリプションを解除することができます。

## <a name="methods-to-manage-data-and-properties"></a>データとプロパティを管理する方法

クライアント アプリケーションは、センサー データを取得できますも**データ フィールド**、または**プロパティ**センサー デバイスに関するメタデータを含んでいます。 サポートされているデータ フィールドまたはプロパティの一覧を取得するセンサー クラスの拡張機能を呼び出す[ **ISensorDriver::OnGetSupportedDataFields** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields)または[ **ISensorDriver::OnGetSupportedProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties)します。 データ フィールドまたはプロパティを取得する値は、クラスの拡張機能の呼び出し[ **ISensorDriver::OnGetDataFields** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields)または[ **ISensorDriver::OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties). プロパティを設定できますが、クラスの拡張機能の呼び出しの[ **ISensorDriver::OnSetProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onsetproperties)新しいプロパティ値を提供します。

## <a name="methods-to-manage-wpd-commands"></a>WPD コマンドを管理する方法

センサー クラスの拡張機能がを介して I/O 制御コマンドを受信したときに[ **ISensorClassExtension::ProcessIoControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol)呼び出しをすることはできません、ハンドラー、 [ **ISensorDriver::OnProcessWpdMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onprocesswpdmessage)します。 このコールバック メソッドは、ドライバーを通知 WPD コマンドが処理されていないと、ドライバー、コマンドを処理する機会が与えられます。 つまり、カスタム WPD コマンドを作成し、ドライバー、センサー プラットフォーム機能を拡張するカスタム ハンドラーを提供できます。

 

 




