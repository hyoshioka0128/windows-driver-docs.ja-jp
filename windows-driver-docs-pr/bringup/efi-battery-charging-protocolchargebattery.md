---
title: EFI_BATTERY_CHARGING_PROTOCOL します。ChargeBattery
description: EFI_BATTERY_CHARGING_PROTOCOL します。ChargeBattery
ms.assetid: 362b812f-b64b-4b6c-84a6-61c09a60f8a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a21f3ab95d77e144a3b4d5808e70f4e9185f7d34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539485"
---
# <a name="efibatterychargingprotocolchargebattery"></a>EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery


最大の料金の現在のターゲットを指定したレベルにメイン バッテリの残量を請求します。

## <a name="syntax"></a>構文


```cpp
typedef EFI_STATUS (EFIAPI * EFI_BATTERY_CHARGING_CHARGE_BATTERY) (
    IN EFI_BATTERY_CHARGING_PROTOCOL *This,
    IN UINT32 MaximumCurrent, 
    IN UINT32 TargetStateOfCharge,
    IN EFI_BATTERY_CHARGING_COMPLETION_TOKEN *CompletionToken );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\] EFI へのポインター\_バッテリ\_充電中\_プロトコル インスタンス。

<a href="" id="maximumcurrent"></a>*MaximumCurrent*  
\[\]省略可能です。 メイン バッテリの充電を使用できる mA の現在の最大です。 NULL 値には、ドライバー自体には、このような詳細を処理するには、このプロトコルを実装するように求められます。

<a href="" id="targetstateofcharge"></a>*TargetStateOfCharge*  
\[\]場合、関数を返しますまでメイン バッテリの充電 (SOC) の状態をターゲット*CompletionToken*は NULL です。 SOC は、完全充電を示す 100% の割合で表されます。

<a href="" id="completiontoken"></a>*CompletionToken*  
\[\]へのポインターを[EFI\_バッテリ\_充電中\_完了\_トークン](efi-battery-charging-completion-token.md)料金が要求された操作に関連付けられています。

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


この非ブロッキング関数では、最大の料金の現在のターゲットを指定したレベルにメイン バッテリの残量が請求されます。

エラーを検出するために、イベントの種類が含まれている*CompletionToken* EVT 必要があります\_通知\_シグナルを使用して作成された**CreateEventEx**と関連付ける必要があります、 **NotifyFunction**で、 *CompletionToken*として**NotifyContext**します。 状態エラー コードが利用する、**状態**のメンバー、 *CompletionToken*します。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック

[EFI\_バッテリ\_充電中\_プロトコル](efi-battery-charging-protocol.md)  

[EFI\_バッテリ\_充電中\_完了\_トークン](efi-battery-charging-completion-token.md)  
