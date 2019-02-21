---
title: DEVPKEY_Device_DHP_Rebalance_Policy
description: DEVPKEY_Device_DHP_Rebalance_Policy
ms.assetid: a882a114-9d1b-41ca-ab24-c2cdda952177
keywords:
- DEVPKEY_Device_DHP_Rebalance_Policy デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DHP_Rebalance_Policy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5e6806250c514a0c823d6bbee58533491ca36fbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536188"
---
# <a name="devpkeydevicedhprebalancepolicy"></a>DEVPKEY_Device_DHP_Rebalance_Policy


DEVPKEY_Device_DHP_Rebalance_Policy デバイスのプロパティがリソースの再均衡化の次に、デバイスが参加するかどうかを示す値を表す、 [(DHP) をパーティション分割、動的なハードウェア](https://msdn.microsoft.com/library/windows/hardware/ff544234)プロセッサ ホット アド操作です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DHP_Rebalance_Policy</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアプリケーションやサービスでのアクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

動的にパーティション分割できるサーバーが実行されているは、Windows Server 2008 またはそれ以降のバージョンの Windows Server では、オペレーティング システムは、新しいプロセッサがシステムに動的に追加されるたびにシステム全体のリソースのバランス調整を開始します。 DEVPKEY_Device_DHP_Rebalance_Policy デバイスのプロパティは、デバイスがこのようなリソースのバランス調整に参加するかどうかを判断します。 デバイスは、次の状況で再調整するリソースに参加します。

-   DEVPKEY_Device_DHP_Rebalance_Policy デバイスのプロパティが存在しません。

-   デバイスのプロパティが存在して、デバイス プロパティの値が設定されていません。

-   デバイスのプロパティが存在して、デバイス プロパティの値が 2 に設定します。

DEVPKEY_Device_DHP_Rebalance_Policy デバイスのプロパティが存在し、プロパティの値が 1 に設定、デバイスは、新しいプロセッサがシステムに動的に追加されたときに再調整するリソースに参加しません。

デバイスの[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)で指定された、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)のデバイスの INF ファイル。

ネットワーク アダプターでのデバイスの既定の動作 (クラス = Net) デバイス セットアップ クラスがクラスのメンバーが、新しいプロセッサがシステムに動的に追加されたときに再調整するリソースに関係しません。 その他のすべてのデバイス セットアップ クラス内のデバイスの既定の動作は、メンバーが新しいプロセッサがシステムに動的に追加されたときに再調整するリソースに含めることです。

このデバイスのプロパティでは、デバイスが他の理由により開始されるリソースのバランス調整に参加するかどうかには影響しません。

DEVPKEY_Device_DHP_Rebalance_Policy プロパティを呼び出すことによってアクセスできる[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)と[ **SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163).

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
<td align="left"><p>Windows Server 2008 および Windows Server の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 






