---
title: HFP デバイスの起動
description: HFP デバイスのスタートアップに関するトピックでは、Bluetooth ハンズフリープロファイル (HFP) デバイスがオーディオシステムに到着した場合の動作について説明します。
ms.assetid: C478BCBA-2A17-4604-AE2B-99B3445C741B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d322f9a5164e5003f59f090ec98f3c4af7446ad9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832356"
---
# <a name="hfp-device-startup"></a>HFP デバイスの起動


HFP デバイスのスタートアップに関するトピックでは、Bluetooth ハンズフリープロファイル (HFP) デバイスがオーディオシステムに到着した場合の動作について説明します。

Windows HFP ドライバーは、オーディオシステムに到着したペアの HFP デバイスごとに、デバイスインターフェイスを GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスクラスに登録します。 オーディオドライバーは、デバイスインターフェイスの通知を使用して、GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスインターフェイスのすべてのインスタンスを常に把握します。 オーディオドライバーは、AVStrMiniDevicePostStart ドライバールーチン (または同等の Portcls ルーチンから) から IoRegisterPlugPlayNotification を呼び出して、現在インストールされている HFP デバイスを検出し、新しい HFP デバイスの通知を受けるコールバックを登録します。

オーディオドライバーが IoRegisterPlugPlayNotification を呼び出すと、次のパラメーターを使用して呼び出しが行われます。

-   EventCategory は EventCategoryDeviceInterfaceChange に設定されています。

-   Eventカテゴリフラグは、通常、既存のインターフェイスの通知を即時に受信するために既存の\_インターフェイス\_含める\_に、PNPNOTIFY\_DEVICE\_INTERFACE に設定されます。 ただし、代替のオーディオドライバーの設計によっては、既存のインターフェイスが他の方法で見つかる場合があります。

-   Eventカテゴリデータは、GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスに設定されます。

-   DriverObject は、オーディオドライバーの DriverObject に設定されます。

-   送信ルーチンは、通知を受信するオーディオドライバーのルーチンに設定されます。

次のセクションでは、ペアリングされた HFP デバイスの登録済みインスタンスごとにオーディオドライバーが実行できるタスクの概要を示します。

## <a name="span-idhandling_interface_instancesspanspan-idhandling_interface_instancesspanspan-idhandling_interface_instancesspanhandling-interface-instances"></a><span id="Handling_interface_instances"></span><span id="handling_interface_instances"></span><span id="HANDLING_INTERFACE_INSTANCES"></span>インターフェイスインスタンスの処理


GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスクラスに登録されているインターフェイスインスタンスごとに、通信に次のプロトコルを使用する必要があります。

オーディオドライバーが IoRegisterPlugPlayNotification という名前で登録されたときに登録されたオーディオドライバーのコールバックルーチンが Windows によって呼び出されると、Windows はデバイス\_インターフェイス\_変更を使用して HFP インターフェイスのシンボリックリンクを渡し\_警告.*SymbolicLinkName*。

オーディオドライバーが IoGetDeviceObjectPointer を呼び出すと、ドライバーはシンボリックリンクを使用して HFP FileObject と HFP デバイスの DeviceObject を取得します。

オーディオドライバーが HFP ドライバーに Ioctl を送信するとき、ドライバーは hfp FileObject と HFP デバイスの DeviceObject を使用します。

## <a name="span-idretrieving_static_informationspanspan-idretrieving_static_informationspanspan-idretrieving_static_informationspanretrieving-static-information"></a><span id="Retrieving_static_information"></span><span id="retrieving_static_information"></span><span id="RETRIEVING_STATIC_INFORMATION"></span>静的な情報の取得


オーディオドライバーは、HFP ドライバーから静的情報を取得できます。 たとえば、HFP ドライバーは、ksnodetype、コンテナー id、およびペアになっている HFP デバイスのフレンドリ名を提供できます。 オーディオドライバーは、この情報を使用して、ペアになっている HFP デバイスを表す KS フィルターまたはフィルターを作成し、初期化することができます。 オーディオドライバーは、この情報を取得するために[ **\_記述子を取得\_ために、IOCTL\_BTHHFP\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)で使用します。

また、オーディオドライバーは、ペアリングされた HFP デバイスの Bluetooth アドレスを取得することもできます。 各 HFP デバイスには一意の Bluetooth アドレスがあり、これは一意の識別子文字列として便利です。 詳細については、「 [HF デバイスの Bluetooth アドレスの取得](obtaining-bluetooth-address-of-hf-device.md)」を参照してください。

## <a name="span-idcreating__initializing_audio-specific_filter_factory_contextspanspan-idcreating__initializing_audio-specific_filter_factory_contextspanspan-idcreating__initializing_audio-specific_filter_factory_contextspancreating-initializing-audio-specific-filter-factory-context"></a><span id="Creating__initializing_audio-specific_filter_factory_context"></span><span id="creating__initializing_audio-specific_filter_factory_context"></span><span id="CREATING__INITIALIZING_AUDIO-SPECIFIC_FILTER_FACTORY_CONTEXT"></span>作成、オーディオ固有のフィルターファクトリコンテキストの初期化


オーディオ固有のフィルターファクトリコンテキストを作成および初期化するには、オーディオドライバーで HFP DeviceObject と HFP FileObject をフィルターファクトリコンテキストに格納し、IsConnected フィールドを false に初期化します。

## <a name="span-idcreating_the_ks_filter_factoryspanspan-idcreating_the_ks_filter_factoryspanspan-idcreating_the_ks_filter_factoryspancreating-the-ks-filter-factory"></a><span id="Creating_the_KS_filter_factory"></span><span id="creating_the_ks_filter_factory"></span><span id="CREATING_THE_KS_FILTER_FACTORY"></span>KS フィルターファクトリの作成


GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスインターフェイスクラスの各デバイスインスタンスに対して、オーディオドライバーによって1つ以上のフィルターファクトリが作成され、有効になります。

オーディオドライバーが AVStream ドライバーの場合、オーディオドライバーは KsCreateFilterFactory を呼び出して新しいフィルターファクトリと KsFilterFactorySetDeviceClassesState を追加し、ファクトリを有効にします。 オーディオドライバーが PortCls ドライバーである場合は、Pcregi サブデバイスを呼び出すことによって、KS フィルターファクトリを間接的に作成し、有効にします。 多くの PortCls オーディオドライバーの設計では、特定のペアの HFP デバイスに2つのサブデバイスが登録されています。

各フィルターファクトリ (または、PortCls オーディオドライバーの場合は、フィルターファクトリの各ペア) は、1つのペアの HFP デバイスのオーディオ機能を表します。 オーディオドライバーは、GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスインターフェイスの一意のインスタンスによって表される、ペアになっている HFP デバイスごとに個別のフィルターファクトリを作成します。 ペアになっている HFP デバイスごとに、オーディオドライバーは KsCreateFilterFactory の*Refstring*パラメーター、または Pcregi サブデバイスの*Name*パラメーターに一意の文字列を使用する必要があります。 ドライバー開発者は、ペアになった HFP デバイスの Bluetooth アドレス文字列を一意の文字列として使用すると便利な場合があります。 一意の文字列を取得する方法については、「 [HF デバイスの Bluetooth アドレスの取得](obtaining-bluetooth-address-of-hf-device.md)」を参照してください。

ペアになっている HFP デバイスの最大数は指定されていないことに注意してください。そのため、オーディオドライバーでは、特定の制限をハードコーディングしないようにする必要があります。 代わりに、オーディオドライバーは、複数の GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスインターフェイスの動的な到着と削除を正しく処理する必要があります。

ただし、実際には、PortCls ドライバーは PcAddAdapterDevice を呼び出すときにサブデバイスの最大数を指定する必要があります。 PcAddAdapterDevice は、潜在的なサブデバイスごとに追加のメモリを事前に割り当てます。 オーディオドライバーの開発者は、ペアになっている多くのデバイスに対応するのに十分な数を選択する必要がありますが、同時に、リソースの無駄にならない数値を選択します。 たとえば、2つの HFP デバイスのみのサポートは不十分であり、2000をサポートすると、リソースが過剰に拡張される可能性があります。 ただし、16をサポートすることは妥当な場合があります。

実行時に、オーディオドライバーに別の GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスインターフェイスが登録されていても、サブデバイスの最大数が既に登録されている場合、オーディオドライバーはいくつかのを呼び出すことができます。新しい HFP デバイス用の領域を確保するために登録を解除できるサブデバイスを含む、ペアリングされた HFP デバイスを選択するアルゴリズム。 たとえば、オーディオドライバーでは、最も古い接続の HFP デバイスを追跡することができます。 それに対して、ユーザーフレンドリなオーディオドライバーは、その最大値に到達した後、より単純ではあるが、\_BLUETOOTH\_HFP\_SCO\_HCIバイパスインターフェイスを使用して、追加の GUID\_単純に無視することもできます。

## <a name="span-idsending_the_get_connection_status_ioctlspanspan-idsending_the_get_connection_status_ioctlspanspan-idsending_the_get_connection_status_ioctlspansending-the-get-connection-status-ioctl"></a><span id="Sending_the_get_connection_status_IOCTL"></span><span id="sending_the_get_connection_status_ioctl"></span><span id="SENDING_THE_GET_CONNECTION_STATUS_IOCTL"></span>Get 接続状態 IOCTL の送信


オーディオドライバーは、get 接続状態 IOCTL を送信して、接続で発生した変更に関する情報を取得します。

## <a name="span-idsending_the_get_volume_status_ioctlspanspan-idsending_the_get_volume_status_ioctlspanspan-idsending_the_get_volume_status_ioctlspansending-the-get-volume-status-ioctl"></a><span id="Sending_the_get_volume_status_IOCTL"></span><span id="sending_the_get_volume_status_ioctl"></span><span id="SENDING_THE_GET_VOLUME_STATUS_IOCTL"></span>Get volume status IOCTL の送信


オーディオドライバーは、get volume status IOCTL を送信して、ヘッドセットのボリュームの状態で発生したボリュームレベルの変更に関する情報を取得します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[**IOCTL\_BTHHFP\_デバイス\_\_記述子を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)  
[操作の理論](theory-of-operation.md)  
[HF デバイスの Bluetooth アドレスを取得しています](obtaining-bluetooth-address-of-hf-device.md)  



