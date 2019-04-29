---
title: EFI_BATTERY_CHARGING_STATUS
description: EFI_BATTERY_CHARGING_STATUS
ms.assetid: dc267920-2c2f-447b-8772-35160886a24c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e9ff65fbcdf645d5617409dda1c05daec26f12f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328018"
---
# <a name="efibatterychargingstatus"></a>EFI\_バッテリ\_充電中\_状態


この列挙体には、バッテリを充電の状態を指定します。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_BATTERY_CHARGING_STATUS {      
    EfiBatteryChargingStatusNone = 0,
    EfiBatteryChargingStatusSuccess,
    EfiBatteryChargingStatusOverheat,
    EfiBatteryChargingStatusVoltageOutOfRange,
    EfiBatteryChargingStatusCurrentOutOfRange,
    EfiBatteryChargingStatusTimeout,
    EfiBatteryChargingStatusAborted,
    EfiBatteryChargingStatusDeviceError,
    EfiBatteryChargingStatusExtremeCold,
    EfiBatteryChargingStatusBatteryChargingNotSupported,
    EfiBatteryChargingStatusBatteryNotDetected,
    EfiBatteryChargingSourceNotDetected,
    EfiBatteryChargingSourceVoltageInvalid,
    EfiBatteryChargingSourceCurrentInvalid,
    EfiBatteryChargingErrorRequestShutdown,
    EfiBatteryChargingErrorRequestReboot
} EFI_BATTERY_CHARGING_STATUS;
```

## <a name="elements"></a>要素


<a href="" id="efibatterychargingstatusnone"></a>EfiBatteryChargingStatusNone  
充電中の状態は、ご利用いただけません。

<a href="" id="efibatterychargingstatussuccess"></a>EfiBatteryChargingStatusSuccess  
操作が完了しました。

<a href="" id="efibatterychargingstatusoverheat"></a>EfiBatteryChargingStatusOverheat  
バッテリの充電を過取得です。

<a href="" id="efibatterychargingstatusvoltageoutofrange"></a>EfiBatteryChargingStatusVoltageOutOfRange  
ロジックを充電するオペレーションの範囲外の電圧が検出されました。

<a href="" id="efibatterychargingstatuscurrentoutofrange"></a>EfiBatteryChargingStatusCurrentOutOfRange  
ロジックの課金には、現在のオペレーションの範囲外が検出されました。

<a href="" id="efibatterychargingstatustimeout"></a>EfiBatteryChargingStatusTimeout  
ロジックの課金には、妥当な時間内、バッテリが充電取得しないことが検出されました。

<a href="" id="efibatterychargingstatusaborted"></a>EfiBatteryChargingStatusAborted  
操作が中止されました。

<a href="" id="efibatterychargingstatusdeviceerror"></a>EfiBatteryChargingStatusDeviceError  
物理デバイスには、エラーが報告されました。

<a href="" id="efibatterychargingstatusextremecold"></a>EfiBatteryChargingStatusExtremeCold  
課金を続行するには、バッテリが寒すぎます。

<a href="" id="efibatterychargingstatusbatterychargingnotsupported"></a>EfiBatteryChargingStatusBatteryChargingNotSupported  
バッテリは充電中の操作をサポートしません。

<a href="" id="efibatterychargingstatusbatterynotdetected"></a>EfiBatteryChargingStatusBatteryNotDetected  
バッテリが検出されません。

<a href="" id="efibatterychargingsourcenotdetected"></a>EfiBatteryChargingSourceNotDetected  
デバイスが充電中のソースに接続されていないし、そのため、充電中の操作を続行できません。

<a href="" id="eefibatterychargingsourcevoltageinvalid"></a>EEfiBatteryChargingSourceVoltageInvalid  
無効な電圧を指定する充電中のソースです。

<a href="" id="efibatterychargingsourcecurrentinvalid"></a>EfiBatteryChargingSourceCurrentInvalid  
無効な現在を指定する充電中のソースです。

<a href="" id="efibatterychargingerrorrequestshutdown"></a>EfiBatteryChargingErrorRequestShutdown  
ドライバーは、システムのシャット ダウンを要求します。

<a href="" id="efibatterychargingerrorrequestreboot"></a>EfiBatteryChargingErrorRequestReboot  
ドライバーは、システムの再起動を要求します。

## <a name="remarks"></a>注釈


EFI\_バッテリ\_充電中\_状態が返された、**状態**のメンバー、 [EFI\_バッテリ\_充電中\_完了\_トークン](efi-battery-charging-completion-token.md)構造体。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック
[EFI\_バッテリ\_充電中\_完了\_トークン](efi-battery-charging-completion-token.md)  



