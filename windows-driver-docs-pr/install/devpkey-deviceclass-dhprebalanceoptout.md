---
title: DEVPKEY_DeviceClass_DHPRebalanceOptOut
description: デバイスのプロパティは、デバイス全体のクラスは、リソースの動的なハードウェア (DHP) をパーティション分割のプロセッサ ホット/追加操作後に再調整に参加するかどうかを示す値を表す DEVPKEY_DeviceClass_DHPRebalanceOptOut が発生しました。プロパティのデータ型を keyDEVPKEY_DeviceClass_DHPRebalanceOptOutProperty identifierDEVPROP_TYPE_BOOLEANProperty accessRead およびアプリケーションやサービスでの書き込みアクセス。ローカライズされたいいえ RemarksOn を実行している Windows Server 2008 または Windows Server オペレーティング システムの開始の以降のバージョン、システム全体のリソースのバランス調整システムに新しいプロセッサが動的に追加されるたびに動的にパーティション分割可能サーバー。 デバイス クラスは、リソース、DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイス プロパティが存在しない次の状況で再均衡化に参加します。デバイスのプロパティが存在して、デバイス プロパティの値が設定されていません。デバイスのプロパティが存在して、デバイス プロパティの値が FALSE に設定します。DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスのプロパティが存在する場合、プロパティの値が TRUE に設定は、デバイス クラスは、新しいプロセッサがシステムに動的に追加されたときに、リソースが再調整には関与しません。デバイスのデバイス セットアップ クラスは、デバイスの INF ファイルの INF セクションで指定されます。(Net クラス) のネットワーク アダプターのこのプロパティの既定値は TRUE です。 その他のすべてのデバイス セットアップ クラスには、このプロパティの既定値は FALSE です。このデバイスのプロパティでは、デバイスのクラスが他の理由により開始されるリソースのバランス調整に参加するかどうかには影響しません。SetupDiGetClassProperty と SetupDiSetClassProperty を呼び出すことによって DEVPKEY_DeviceClass_DHPRebalanceOptOut プロパティにアクセスすることができます。
ms.assetid: e620ef24-b65d-4cf6-a21d-ffecad5804b4
keywords:
- DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DHPRebalanceOptOut
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f689dd3447396744193eac9c82cb607fd307e69c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378079"
---
# <a name="devpkeydeviceclassdhprebalanceoptout"></a>DEVPKEY_DeviceClass_DHPRebalanceOptOut


DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスのプロパティは、デバイス全体のクラスは、リソースの後に再調整に参加するかどうかを示す値を表す、 [(DHP) をパーティション分割、動的なハードウェア](https://docs.microsoft.com/windows-hardware/drivers/kernel/dynamic-hardware-partitioning-techniques)プロセッサホット アド操作が発生しました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_DHPRebalanceOptOut</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
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

 

**注釈**

動的にパーティション分割できるサーバーが実行されているは、Windows Server 2008 またはそれ以降のバージョンの Windows Server では、オペレーティング システムは、新しいプロセッサがシステムに動的に追加されるたびにシステム全体のリソースのバランス調整を開始します。 デバイス クラスは、次の状況で再調整するリソースに参加します。

-   DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスのプロパティが存在しません。

-   デバイスのプロパティが存在して、デバイス プロパティの値が設定されていません。

-   デバイスのプロパティが存在して、デバイス プロパティの値に設定されます**FALSE**します。

DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスのプロパティが存在する場合、プロパティの値に設定されます**TRUE**デバイスのクラスは、新しいプロセッサが動的に追加する場合に再調整するリソースに関与しません、システム。

デバイスの[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)で指定された、 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)のデバイスの INF ファイル。

ネットワーク アダプターのこのプロパティの既定値 (クラス = Net) は**TRUE**します。 その他のすべてのデバイス セットアップ クラスには、このプロパティの既定値は**FALSE**します。

このデバイスのプロパティでは、デバイスのクラスが他の理由により開始されるリソースのバランス調整に参加するかどうかには影響しません。

DEVPKEY_DeviceClass_DHPRebalanceOptOut プロパティを呼び出すことによってアクセスできる[ **SetupDiGetClassProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)と[ **SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw).

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


[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

 

 






