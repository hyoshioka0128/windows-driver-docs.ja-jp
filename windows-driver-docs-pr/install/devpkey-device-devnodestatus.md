---
title: DEVPKEY_Device_DevNodeStatus
description: DEVPKEY_Device_DevNodeStatus
ms.assetid: 538a78f0-c704-444e-8314-38b2e0421c39
keywords:
- DEVPKEY_Device_DevNodeStatus デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DevNodeStatus
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f96c67447927809b7881a9eb0b3166bd247e6958
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387085"
---
# <a name="devpkeydevicedevnodestatus"></a>DEVPKEY_Device_DevNodeStatus


DEVPKEY_Device_DevNodeStatus デバイスのプロパティは、[デバイス] ノードの状態を表します (*devnode*)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DevNodeStatus</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_DevNodeStatus の値は、DN_ のビットごとの OR*Xxx* Cfg.h で定義されているフラグのビットします。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) DEVPKEY_Device_DevNodeStatus の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティを直接サポートされません。 以前のバージョンの Windows 上のデバイスのインスタンスの状態にアクセスする方法については、次を参照してください。[デバイス インスタンスの状態と問題のコードを取得する](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-the-status-and-problem-code-for-a-device-instance)します。

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
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






