---
title: DEVPKEY_Device_ProblemCode
description: DEVPKEY_Device_ProblemCode
ms.assetid: 545fb6f7-660e-4df8-80cd-48b36910a518
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_ProblemCode
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ProblemCode
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 02/28/2020
ms.openlocfilehash: 223d5e811b400f1aa0869a43a382c6f2101c39bb
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418465"
---
# <a name="devpkey_device_problemcode"></a>DEVPKEY_Device_ProblemCode


DEVPKEY_Device_ProblemCode デバイスプロパティは、デバイスインスタンスの問題コードを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ProblemCode</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_ProblemCode の値は、Cfg に定義されている CM_PROB_*Xxx*問題コードの1つです。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_ProblemCode の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティは直接サポートされていません。 以前のバージョンの Windows 上にあるデバイスインスタンスの問題コードにアクセスする方法の詳細については、「[デバイスインスタンスの状態と問題コードを取得](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-the-status-and-problem-code-for-a-device-instance)する」を参照してください。

デバイスマネージャーまたはカーネルデバッガーで問題の状態を検出する方法の詳細については、「[デバイスインスタンスの状態と問題のコードを取得](retrieving-the-status-and-problem-code-for-a-device-instance.md)する」を参照してください。

問題コードの詳細については、「 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)

 






