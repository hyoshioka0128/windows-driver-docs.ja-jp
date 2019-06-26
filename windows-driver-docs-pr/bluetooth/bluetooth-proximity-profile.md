---
title: Bluetooth 近接通信プロファイル
description: 近接プロファイルは、その近接性を検出するためにデバイスを許可するためのもので、2 つのロールを定義します。
ms.assetid: 6BA67CA4-AAE4-4D01-97A4-65970704E7ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37466465999a8bc5569f2bfb4d15d4a807214b34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354045"
---
# <a name="bluetooth-proximity-profile"></a>Bluetooth 近接通信プロファイル


近接プロファイルは、その近接性を検出するためにデバイスを許可するためのもので、2 つのロールを定義します。

2 つのロールが呼び出されます。

-   近接レポーター
-   近接モニター

![ロールのリレーションシップ](images/bthleproximityroles.png)

## <a name="span-idproximityreporterspanspan-idproximityreporterspanspan-idproximityreporterspanproximity-reporter"></a><span id="Proximity_Reporter"></span><span id="proximity_reporter"></span><span id="PROXIMITY_REPORTER"></span>近接レポーター


GATT サーバーにするには、近接性レポーターが必要です。

近接レポーターは、次の GATT サービスをサポートしています。

-   リンクの損失サービス (必須)
-   即時の通知サービス (省略可能)
-   Tx Power サービス (省略可能)

## <a name="span-idproximitymonitorspanspan-idproximitymonitorspanspan-idproximitymonitorspanproximity-monitor"></a><span id="Proximity_Monitor"></span><span id="proximity_monitor"></span><span id="PROXIMITY_MONITOR"></span>近接モニター


近接モニターが、GATT クライアントです。 作成、シグナルのパスの損失を計算する接続の近接性レポーターとモニター、ラジオの信号強度情報への接続 (または RSSI) を維持し、する必要があります。 省略可能な「Tx Power サービス」が近接レポーターで使用可能な場合は、テキサス州の電力レベルから RSSI を差し引いて RSSI 値を正規化するこの追加情報も使用できます。

## <a name="span-idsupportforgattinwindows81spanspan-idsupportforgattinwindows81span-support-for-gatt-in-windows81"></a><span id="_support_for_gatt_in_windows_8.1"></span><span id="_SUPPORT_FOR_GATT_IN_WINDOWS_8.1"></span> Windows 8.1 で GATT のサポート


GATT デバイスは、Windows 8.1 と組み合わせると、デバイス、システムの一部になるし、Windows が提供されます*デバイス オブジェクト*デバイスと、デバイスによって報告された、プライマリ サービスの両方を表します。

[ **Windows.Devices.Bluetooth.GenericAttributeProfile 名前空間**](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile)します。 アプリ開発者は、Windows 8.1 で使用できる汎用の属性のプロファイル Api について説明します。

デバイス アプリを開発する際に、最初の手順の 1 つは、Bluetooth サービスをユーザーが関心のシナリオを実現するためにアプリのニーズを特定します。 近接プロファイルでは、デバイス アプリは、「リンクが失われるサービス」と必要に応じて「即時警告サービス」と"Tx Power Service"を使用する必要があります。

かどうか、デバイスとペアに Windows の実装「リンクが失われるサービス」を確認するデバイス アプリのために、アプリがで利用できる Api を使用する必要があります、 [ **Windows.Devices.Enumeration 名前空間**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)、namely DeviceInformation.FindAllAsync メソッド。

[ **DeviceInformation.FindAllAsync メソッド**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_FindAllAsync_System_String_)は、 *AQS (高度なクエリ構文)* デバイス セレクターが含まれているデバイスのみをフィルター処理するためにパラメーターとして、"リンクの損失サービス"。 デバイス アプリの開発者が使用することも、 [ **GetDeviceSelectorFromUuid** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_GetDeviceSelectorFromUuid_System_Guid_)または[ **GetDeviceSelectorFromShortId** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_GetDeviceSelectorFromShortId_System_UInt16_) のメソッド[**GattDeviceService** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService)クラス、AQS フィルターを手動で作成しないで済むようにします。

「リンクが失われるサービス」は、Bluetooth SIG、およびように定義されている Bluetooth GATT サービス、*短い Id*の代わりに使用できる、 *UUID の完全修飾*します。

*短い Id*近接のプロファイル サービスに割り当てられているサービス Id には。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サービス名</th>
<th align="left">短い Id</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>リンクの損失</p></td>
<td align="left"><p>0x1803</p></td>
</tr>
<tr class="even">
<td align="left"><p>即時のアラート</p></td>
<td align="left"><p>0x1802</p></td>
</tr>
<tr class="odd">
<td align="left"><p>テキサス州の電源</p></td>
<td align="left"><p>0x1804</p></td>
</tr>
</tbody>
</table>

 

Bluetooth SIG の維持の日付まで最も[サービスの一覧](https://go.microsoft.com/fwlink/p/?linkid=320723)します。

オブジェクトが使用する開発者がどのサービスを決定した後は、オブジェクトを呼び出すことができます[ **GattDeviceService.FromIdAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_FromIdAsync_System_String_)サービスのインスタンスを取得します。

開発者が、有効な GattDeviceService オブジェクトを取得した後は、デバイスを使用して、通信に使用されますができます、 [ **Windows.Devices.Bluetooth.GenericAttributeProfile** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile) API。

これらの Api は、特定のサービスとそれらのオブジェクト (に含まれるサービス、特性、および記述子など) へのアクセスを有効にするだけでなく読み取りおよび書き込み機能。

[Bluetooth ジェネリック属性プロファイル - 心拍サービス](https://go.microsoft.com/fwlink/p/?linkid=301978)サンプルでは、これらの手法の一部を示します。

## <a name="span-idusingpowerefficientlyspanspan-idusingpowerefficientlyspanspan-idusingpowerefficientlyspanusing-power-efficiently"></a><span id="Using_Power_Efficiently"></span><span id="using_power_efficiently"></span><span id="USING_POWER_EFFICIENTLY"></span>電源を効率的に使用します。


Windows 8.1 での Bluetooth 低エネルギーのサポートには、電源を効率的を使用して強力なフォーカスがあります。 これには、ローカル Bluetooth 無線アダプターの電力消費の削減とできるだけ少なくする CPU の使用が含まれます。

したがって、Bluetooth LE 接続を確立するために、アプリに必要なハンドラーを登録、 [ **GattCharacteristic.ValueChanged** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_ValueChanged)イベント。 または、アプリが呼び出す必要がありますのいずれか、 [ **GattCharacteristic.ReadValueAsync**](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_ReadValueAsync_Windows_Devices_Bluetooth_BluetoothCacheMode_)、 [ **GattCharacteristic.WriteValueAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_WriteValueAsync_Windows_Storage_Streams_IBuffer_)または[ **GattCharacteristic.WriteClientCharacteristicConfigurationDescriptorAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_WriteClientCharacteristicConfigurationDescriptorAsync_Windows_Devices_Bluetooth_GenericAttributeProfile_GattClientCharacteristicConfigurationDescriptorValue_) BluetoothCacheMode.Cached オプションを指定せずメソッド。

**注**  電力消費量を最小限に抑えるために Windows がアクティブに監視のリンクの RSSI 値ローカル Bluetooth 無線コントローラをポーリングしています。

 

電源に関する注意事項が記載されて[近接プロファイル実装の詳細](proximity-profile-implementation-details.md)します。

 

 





