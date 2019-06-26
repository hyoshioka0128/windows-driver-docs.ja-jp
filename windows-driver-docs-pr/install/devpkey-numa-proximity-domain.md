---
title: DEVPKEY_Numa_Proximity_Domain
description: DEVPKEY_Numa_Proximity_Domain
ms.assetid: 384e167b-cb08-4264-a7b1-3cea2dda0d46
keywords:
- DEVPKEY_Numa_Proximity_Domain デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Numa_Proximity_Domain
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9c24e1a67d6523642224bdf2854c9b03b7614996
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376806"
---
# <a name="devpkeynumaproximitydomain"></a>DEVPKEY_Numa_Proximity_Domain


DEVPKEY_Numa_Proximity_Domain デバイス プロパティは、近接、Non-uniform Memory アーキテクチャ (NUMA) のドメインを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Numa_Proximity_Domain</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールしてインストーラー; 読み取り専用アクセス読み取り/書き込みアクセスでデバイス ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Numa_Proximity_Domain 値とは、ドメイン ID を表す数値です。

通常、オペレーティング システムでは、システム ファームウェアから対応する情報を取得して DEVPKEY_Numa_Proximity_Domain の値を設定します。

DEVPKEY_Numa_Proximity_Domain の値を取得するには呼び出すことによって**IoSetDevicePropertyData**または**IoGetDevicePropertyData**のデバイス ドライバーにします。

呼び出すこともできます[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) DEVPKEY_Numa_Proximity_Domain の値を取得します。

このプロパティの値は、Windows が所有し、ドライバーとアプリケーションで読み取り専用として扱う必要があります。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされません。

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
<td align="left"><p>Windows Vista 以降で利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

 

 





