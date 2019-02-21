---
title: EFI_BATTERY_CHARGING_PROTOCOL します。GetBatteryStatus
description: EFI_BATTERY_CHARGING_PROTOCOL します。GetBatteryStatus
ms.assetid: dc2b647b-b3b6-4d85-9faf-9e401fa67571
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6159f4fea5db4361067d0ec066a5574b9f393df8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549895"
---
# <a name="efibatterychargingprotocolgetbatterystatus"></a>EFI\_バッテリ\_充電中\_プロトコル。GetBatteryStatus


メイン バッテリの現在の状態に関する情報を返します。

## <a name="syntax"></a>構文


```cpp
typedef EFI_STATUS (EFIAPI * EFI_BATTERY_CHARGING_GET_BATTERY_STATUS) (
    IN EFI_BATTERY_CHARGING_PROTOCOL *This,
    OUT UINT32 *StateOfCharge,
    OUT UINT32 *RatedCapacity,
    OUT INT32 *ChargeCurrent );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\] EFI へのポインター\_バッテリ\_充電中\_プロトコル インスタンス。

<a href="" id="stateofcharge"></a>*StateOfCharge*  
\[out\]メイン バッテリの充電 (SOC) の現在の状態を返します。 SOC は、完全充電を示す 100% の割合で表されます。

<a href="" id="ratedcapacity"></a>*RatedCapacity*  
\[out\] mAh でメインのバッテリの定格容量を返します。

<a href="" id="chargecurrent"></a>*ChargeCurrent*  
\[out\]バッテリが充電中であるにある場合は、現在の mA のバッテリに配信されることを示す正の数を返します。 バッテリが放電中であるにある場合は、現在の mA のバッテリから描画されていることを示す、負の数を返します。 バッテリが充電中も、放電中の場合は、0 を返します。 EFI を返しますが、ハードウェアがこの情報を提供できない場合は、\_バッテリ\_料金\_現在\_いない\_(0x80000000) サポートされています。

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


この関数は、評価済みの容量とメイン バッテリの充電 (SOC) の状態を返します。 この関数は定期的に支援するためにこのプロトコルを実装するドライバーによる追加の処理します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック
[EFI\_バッテリ\_充電中\_プロトコル](efi-battery-charging-protocol.md)  



