---
title: HFP デバイスの起動
description: HFP デバイスの起動トピックでは、Bluetooth ハンズフリー プロファイル (HFP) デバイスは、オーディオ システムに到着したときの動作について説明します。
ms.assetid: C478BCBA-2A17-4604-AE2B-99B3445C741B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13434323205ff001db3eb1105ecfd2c5817ed878
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328606"
---
# <a name="hfp-device-startup"></a>HFP デバイスの起動


HFP デバイスの起動トピックでは、Bluetooth ハンズフリー プロファイル (HFP) デバイスは、オーディオ システムに到着したときの動作について説明します。

Windows HFP ドライバー、オーディオ システムに到着する各ペアになっている HFP デバイス、GUID でデバイスのインターフェイスを登録します\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS クラス。 オーディオ ドライバーでは、デバイス インターフェイスの通知を使用して、すべてのインスタンスの GUID を把握\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS インターフェイス。 その AVStrMiniDevicePostStart ドライバー ルーチン内 (または同等の Portcls ルーチンから)、オーディオ ドライバーがから IoRegisterPlugPlayNotification を呼び出し、現在インストールされている HFP デバイスの検出と、新しい HFP デバイスの通知コールバックを登録します。

オーディオ ドライバー IoRegisterPlugPlayNotification を呼び出すと、呼び出しが、次のパラメーターを使用して行われます。

-   によっては、EventCategoryDeviceInterfaceChange に設定されます。

-   EventCategoryFlags が通常 PNPNOTIFY に設定されている\_デバイス\_インターフェイス\_INCLUDE\_既存\_既存のインターフェイスの即時の通知を受信するにはインターフェイスです。 ただし、代替オーディオ ドライバーを設計他の手段で既存のインターフェイスがあります。

-   GUID に設定されている EventCategoryData\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS します。

-   DriverObject は、オーディオ ドライバーの DriverObject に設定されます。

-   CallbackRoutine は、通知を受信するオーディオ ドライバー内のルーチンに設定されます。

次のセクションではアウトライン ペアになる HFP デバイスの登録済みのインスタンスごとのオーディオ ドライバーの可能なタスクを実行します。

## <a name="span-idhandlinginterfaceinstancesspanspan-idhandlinginterfaceinstancesspanspan-idhandlinginterfaceinstancesspanhandling-interface-instances"></a><span id="Handling_interface_instances"></span><span id="handling_interface_instances"></span><span id="HANDLING_INTERFACE_INSTANCES"></span>インターフェイスのインスタンスの処理


GUID に登録されているインターフェイスのインスタンスごとに\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS クラス、オーディオ ドライバーは、次のプロトコルを通信に使用する必要があります。

Windows オーディオ ドライバーに IoRegisterPlugPlayNotification が呼び出されたときに登録された、オーディオ ドライバーのコールバック ルーチンを呼び出すと Windows 渡します HFP インターフェイスのシンボリック リンクをデバイスを使用して\_インターフェイス\_の変更\_通知します。*SymbolicLinkName*します。

オーディオ ドライバー IoGetDeviceObjectPointer を呼び出すと、ドライバーは HFP FileObject と HFP デバイスのデバイス オブジェクトを取得するのにシンボリック リンクを使用します。

オーディオ ドライバーでは、Ioctl を HFP ドライバーに送信するときに、ドライバーは HFP デバイス HFP FileObject と、デバイス オブジェクトを使用します。

## <a name="span-idretrievingstaticinformationspanspan-idretrievingstaticinformationspanspan-idretrievingstaticinformationspanretrieving-static-information"></a><span id="Retrieving_static_information"></span><span id="retrieving_static_information"></span><span id="RETRIEVING_STATIC_INFORMATION"></span>静的な情報を取得します。


オーディオ ドライバーでは、HFP ドライバーからの静的な情報を取得できます。 たとえば、HFP ドライバーでは、ksnodetype、コンテナー id とペアになる HFP デバイスのフレンドリ名を提供できます。 オーディオ ドライバーでは、作成し、初期化 KS フィルターまたはフィルターを表すペアになる HFP デバイスをこの情報を使用できます。 オーディオ ドライバーを使用して[ **IOCTL\_BTHHFP\_デバイス\_取得\_記述子**](https://msdn.microsoft.com/library/windows/hardware/dn265108)この情報を取得します。

オーディオ ドライバーには、ペアになっている HFP デバイスの Bluetooth アドレスも取得できます。 各ペアになっている HFP デバイスが Bluetooth の一意のアドレスと、これは、一意の識別子の文字列として役立ちます。 詳細については、次を参照してください。 [HF デバイスの Bluetooth のアドレスを取得する](obtaining-bluetooth-address-of-hf-device.md)します。

## <a name="span-idcreatinginitializingaudio-specificfilterfactorycontextspanspan-idcreatinginitializingaudio-specificfilterfactorycontextspanspan-idcreatinginitializingaudio-specificfilterfactorycontextspancreating-initializing-audio-specific-filter-factory-context"></a><span id="Creating__initializing_audio-specific_filter_factory_context"></span><span id="creating__initializing_audio-specific_filter_factory_context"></span><span id="CREATING__INITIALIZING_AUDIO-SPECIFIC_FILTER_FACTORY_CONTEXT"></span>作成すると、オーディオ固有のフィルターの工場出荷時のコンテキストを初期化しています


作成し、オーディオ固有のフィルターの工場出荷時のコンテキストを初期化、オーディオ ドライバーはフィルターの工場出荷時のコンテキストで HFP デバイス オブジェクトと HFP FileObject を格納する必要があり、IsConnected フィールドを false に初期化します。

## <a name="span-idcreatingtheksfilterfactoryspanspan-idcreatingtheksfilterfactoryspanspan-idcreatingtheksfilterfactoryspancreating-the-ks-filter-factory"></a><span id="Creating_the_KS_filter_factory"></span><span id="creating_the_ks_filter_factory"></span><span id="CREATING_THE_KS_FILTER_FACTORY"></span>KS フィルター ファクトリの作成


各デバイス インスタンス GUID で\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS インターフェイス クラス、オーディオ ドライバーは、作成し、1 つまたは複数のフィルター ファクトリを有効にします。

オーディオ ドライバーが、AVStream ドライバーの場合は、オーディオ ドライバーは、KsCreateFilterFactory 新しいフィルター ファクトリを追加して、ファクトリを有効にする KsFilterFactorySetDeviceClassesState を呼び出します。 場合 PortCls オーディオ ドライバーには、間接的に作成し、PcRegisterSubdevice を呼び出すことにより、KS フィルター ファクトリ。 多くの PortCls オーディオ ドライバー設計の特定のペアになっている HFP デバイスの登録されている 2 つのサブ デバイスがあります。

各フィルター ファクトリ (または PortCls オーディオ ドライバー、フィルター ファクトリの各ペアを) 1 つのペアになっている HFP デバイスのオーディオ機能を表します。 オーディオ ドライバーは、GUID の一意のインスタンスによって表されるペアになっている HFP デバイスごとに別個のフィルター ファクトリを作成します。\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS インターフェイス。 オーディオ ドライバー ペアになっている HFP デバイスごとの一意の文字列を使用する必要があります、 *RefString* KsCreateFilterFactory のパラメーターまたは*名前*PcRegisterSubdevice のパラメーター。 ドライバー開発者は、それに役に立つ一意の文字列として、ペアになっている HFP デバイスの Bluetooth アドレス文字列を使用します。 参照してください[HF デバイスの Bluetooth のアドレスを取得する](obtaining-bluetooth-address-of-hf-device.md)一意の文字列を取得する方法についてはします。

オーディオ ドライバーでは、特定の制限をハード コーディングしないようにする必要がありますので、可能なペアになっている HFP デバイスの最大数を特定しないことに注意してください。 代わりに、オーディオ ドライバーする必要がありますを正しく処理 GUID の複数の削除と動的な到着\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS インターフェイス。

実際には、ただし、PortCls ドライバーする必要があります指定サブのデバイスの最大数 PcAddAdapterDevice を呼び出すときにします。 PcAddAdapterDevice 潜在的なサブ デバイスごとに余分なメモリを事前に割り当てます。 オーディオ ドライバー開発者は、高、対になった多数のデバイスに対応が同時に、リソースが無駄にすることはない数値を選択します。 数値を選択する必要があります。 たとえば、HFP デバイスで 2 つだけサポートできない可能性があります、適切なと過多のリソースに確実に結果は 2000 をサポートしています。 ただし、16 のサポートは、妥当である可能性があります。

別の GUID の実行時に、オーディオ ドライバーが通知された場合\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS インターフェイスしますが、サブのデバイスの最大数が既に登録されている、オーディオ ドライバーには、ペアになっている HFP デバイス新しい HFP デバイス確保するために、登録を解除できますサブ デバイスを選択するいくつかのアルゴリズムを呼び出すことができます。 たとえば、オーディオ ドライバーでしたの追跡、最も古い接続 HFP デバイス。 一方、オーディオ ドライバーのわかりやすいことはおそらくあまり簡単でした追加の GUID を単純に無視\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_の上限に達した後 HCIBYPASS インターフェイス。

## <a name="span-idsendingthegetconnectionstatusioctlspanspan-idsendingthegetconnectionstatusioctlspanspan-idsendingthegetconnectionstatusioctlspansending-the-get-connection-status-ioctl"></a><span id="Sending_the_get_connection_status_IOCTL"></span><span id="sending_the_get_connection_status_ioctl"></span><span id="SENDING_THE_GET_CONNECTION_STATUS_IOCTL"></span>IOCTL get 接続の状態を送信します。


オーディオ ドライバーでは、IOCTL、接続で発生したすべての変更に関する情報を取得する get 接続の状態を送信します。

## <a name="span-idsendingthegetvolumestatusioctlspanspan-idsendingthegetvolumestatusioctlspanspan-idsendingthegetvolumestatusioctlspansending-the-get-volume-status-ioctl"></a><span id="Sending_the_get_volume_status_IOCTL"></span><span id="sending_the_get_volume_status_ioctl"></span><span id="SENDING_THE_GET_VOLUME_STATUS_IOCTL"></span>IOCTL get ボリュームの状態を送信します。


オーディオ ドライバーでは、IOCTL、ヘッドセットのボリュームの状態で発生したボリューム レベルでの変更に関する情報を取得する get ボリュームの状態を送信します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/dn265108)  
[操作の理論を概説します。](theory-of-operation.md)  
[HF デバイスの Bluetooth のアドレスを取得します。](obtaining-bluetooth-address-of-hf-device.md)  



