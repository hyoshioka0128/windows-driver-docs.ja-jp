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
ms.openlocfilehash: 83230d0ab8bf01d6d16b23c0c7e16972946f5514
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279449"
---
# <a name="devpkey_device_problemcode"></a>DEVPKEY_Device_ProblemCode


DEVPKEY_Device_ProblemCode デバイスプロパティは、デバイスインスタンスの問題コードを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>プロパティアクセス</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

DEVPKEY_Device_ProblemCode の値は、Cfg に定義されている CM_PROB_*Xxx*問題コードの1つです。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_ProblemCode の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティは直接サポートされていません。 以前のバージョンの Windows 上にあるデバイスインスタンスの問題コードにアクセスする方法の詳細については、「[デバイスインスタンスの状態と問題コードを取得](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-the-status-and-problem-code-for-a-device-instance)する」を参照してください。

デバイスマネージャーまたはカーネルデバッガーで問題の状態を検出する方法の詳細については、「[デバイスインスタンスの状態と問題のコードを取得](retrieving-the-status-and-problem-code-for-a-device-instance.md)する」を参照してください。

問題コードの詳細については、「 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)」を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>参照


[**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)

 






