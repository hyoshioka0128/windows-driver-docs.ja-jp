---
title: EFI_BATTERY_CHARGING_PROTOCOL
description: EFI_BATTERY_CHARGING_PROTOCOL
ms.assetid: 978d063e-f864-44be-9f58-4e4c6b2193b8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff284993c68a58ac7635225fbdb32148f5ab7758
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537824"
---
# <a name="efibatterychargingprotocol"></a>EFI\_バッテリ\_充電中\_プロトコル


このプロトコルには、メイン バッテリの充電をサポートするために、UEFI ドライバーができます。

## <a name="syntax"></a>構文


```cpp
// {840CB643-8198-428a-A8B3-A072CE57CDB9}
#define EFI_BATTERY_CHARGING_PROTOCOL_GUID \
  {0x840cb643, 0x8198, 0x428a, 0xa8, 0xb3, 0xa0, 0x72, 0xce, 0x57, 0xcd, 0xb9};

typedef struct _EFI_BATTERY_CHARGING_PROTOCOL {
  EFI_BATTERY_CHARGING_GET_BATTERY_STATUS         GetBatteryStatus;
  EFI_BATTERY_CHARGING_CHARGE_BATTERY             ChargeBattery; 
  UINT32                                          Revision;
  EFI_BATTERY_CHARGING_GET_BATTERY_INFORMATION    GetBatteryInformation;
} EFI_BATTERY_CHARGING_PROTOCOL;
```

## <a name="members"></a>Members


<a href="" id="getbatterystatus"></a>**GetBatteryStatus**  
メイン バッテリの現在の状態に関する情報を返します。

<a href="" id="chargebattery"></a>**ChargeBattery**  
指定した最大現在を使用して、指定されたレベルにメイン バッテリの残量を請求します。

<a href="" id="revision"></a>**リビジョン**  
リビジョンを EFI\_バッテリ\_充電中\_プロトコルに準拠します。 すべての将来のリビジョンは、旧バージョンと互換性のあるである必要があります。 場合は、今後のバージョンは旧バージョンと互換性のある、別の GUID を使用する必要があります。

現在のリビジョンは 0x00010002、リビジョン 0x00010001 もサポートされています。 詳細については、プロトコルの各バージョンでどの関数がサポートされている、以下の「解説」セクションを参照してください。

<a href="" id="getbatteryinformation"></a>**GetBatteryInformation**  
メイン バッテリの現在の状態に関する情報を返します。 この機能に似ています**GetBatteryStatus**より多くの情報を提供しますが、 **GetBatteryStatus**します。

## <a name="remarks"></a>注釈


次の表は、EFI の各バージョンでサポートされている関数\_バッテリ\_充電中\_プロトコル。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リビジョン 0x00010002</th>
<th>リビジョン 0x00010001</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>GetBatteryInformation</strong></p>
<p><strong>GetBatteryStatus</strong></p>
<p><strong>ChargeBattery</strong></p></td>
<td><p><strong>GetBatteryStatus</strong></p>
<p><strong>ChargeBattery</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック

[UEFI のバッテリ充電プロトコル](uefi-battery-charging-protocol.md)  

[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)  

[EFI\_バッテリ\_充電中\_プロトコル。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)  

[EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)  
