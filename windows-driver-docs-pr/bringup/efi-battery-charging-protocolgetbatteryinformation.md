---
title: EFI_BATTERY_CHARGING_PROTOCOL します。GetBatteryInformation
description: EFI_BATTERY_CHARGING_PROTOCOL します。GetBatteryInformation
ms.assetid: 497cd001-5180-4dee-a070-ccf8c987bd71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de0470ff8a3f6dc41c366d6a4d04f30102edb0e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559082"
---
# <a name="efibatterychargingprotocolgetbatteryinformation"></a>EFI\_バッテリ\_充電中\_プロトコル。GetBatteryInformation


料金に配信したり、バッテリ、バッテリの端末、バッテリ温度、USB ケーブルを電圧にわたる電圧外に描画されている現在の状態を含むメイン バッテリの現在の状態に関する情報を返します現在の USB ケーブルを使用します。

## <a name="syntax"></a>構文


```cpp
typedef EFI_STATUS (EFIAPI * EFI_BATTERY_CHARGING_GET_BATTERY_INFORMATION) (
    IN EFI_BATTERY_CHARGING_PROTOCOL *This,
    OUT UINT32 *StateOfCharge,
    OUT INT32 *CurrentIntoBattery,
    OUT UINT32 *BatteryTerminalVoltage, 
    OUT INT32 *BatteryTemperature,
    OUT UINT32 *USBCableVoltage,
    OUT UINT32 *USBCableCurrent );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\] EFI へのポインター\_バッテリ\_充電中\_プロトコル インスタンス。

<a href="" id="stateofcharge"></a>*StateOfCharge*  
\[out\]メイン バッテリの充電 (SOC) の現在の状態を返します。 SOC は 100% が完全に充電を示す割合で表されます。

<a href="" id="currentintobattery"></a>*CurrentIntoBattery*  
\[out\]次の表に示す、値のいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>正の数</p></td>
<td><p>バッテリは、課金される予定です。 値は、現在の mA のバッテリに配信を示します。</p></td>
</tr>
<tr class="even">
<td><p>負の数</p></td>
<td><p>バッテリは放電中です。 MA のバッテリから描画されている現在の値を示します。</p></td>
</tr>
<tr class="odd">
<td><p>0</p></td>
<td><p>対象外のバッテリ充電、または放電です。</p></td>
</tr>
<tr class="even">
<td><p>EFI_BATTERY_CHARGE_CURRENT_NOT_SUPPORTED (0x80000000)</p></td>
<td><p>ハードウェアは、この情報を提供することができます。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="batteryterminalvoltage"></a>*BatteryTerminalVoltage*  
\[out\] mV でバッテリ端末間で電圧します。

<a href="" id="batterytemperature"></a>*BatteryTemperature*  
\[out\]ケルビン度の 10ths のバッテリの温度。

<a href="" id="usbcablevoltage"></a>*USBCableVoltage*  
\[out\]電圧 mV の USB ケーブルを経由します。

<a href="" id="usbcablecurrent"></a>*USBCableCurrent*  
\[out\]現在の mA の USB ケーブルを使用します。

## <a name="return-value"></a>戻り値


次のステータス コードのいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>関数が正常に返されます。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>パラメーターが正しくありません。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理デバイスには、エラーが報告されました。</p></td>
</tr>
<tr class="even">
<td><p>EFI_NOT_READY</p></td>
<td><p>物理デバイスは、ビジー状態か、この要求を処理する準備ができていません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


この関数は、UEFI のバッテリ充電バッテリに関する情報を取得するアプリケーションによって定期的に呼び出されます。 アプリケーションでは、この情報を使用して、バッテリの状態を監視し、エラーを診断に役立ちます。

**注**  この関数は、EFI のリビジョン 0x00010002 以降使用可能な\_バッテリ\_充電中\_プロトコル。 UEFI バッテリが充電アプリケーションでは、専用プロトコルのリビジョン 0x00010001 が利用可能なことを呼び出すことが検出された場合[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)代わりにします。

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック
[EFI\_バッテリ\_充電中\_プロトコル](efi-battery-charging-protocol.md)  



