---
title: DEVPKEY_DeviceClass_DevType
description: DEVPKEY_DeviceClass_DevType
ms.assetid: 383f2b47-c0ee-49c2-851c-b18c98fd0303
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_DevType
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DevType
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e11e4ec58a40dbdcf53c69ba2f90436f0a6283dd
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418540"
---
# <a name="devpkey_deviceclass_devtype"></a>DEVPKEY_DeviceClass_DevType


DEVPKEY_DeviceClass_DevType デバイスプロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)の既定のデバイスの種類を表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_DevType</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>デバイスセットアップクラスがインストールされた後のインストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_DEVTYPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

インストールアプリケーションがデバイスセットアップクラスをインストールするときに DEVPKEY_DeviceClass_DevType の値を設定できます。 デバイスセットアップクラスをインストールし、このプロパティを設定する方法の詳細については、「 [**Inf ClassInstall32」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)と、「 [**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」の「特別な*値-エントリ名*のキーワード」セクションに記載されているレジストリエントリ値 **(devicetype**に関する情報を参照してください。

DEVPKEY_DeviceClass_DevType の値は、Wdm および Ntddk で定義されている FILE_DEVICE_Xxx 値の1つです。 デバイスの種類の詳細については、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)関数の *(devicetype*パラメーターを参照してください。

[**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出して、DEVPKEY_DeviceClass_DevType の値を取得できます。

Windows Server 2003 および Windows XP では、このプロパティはサポートされていますが、DEVPKEY_DeviceClass_DevType のプロパティキーはサポートされていません。 以前のバージョンの Windows では、SPCRP_DEVTYPE 識別子を使用して、このプロパティの値にアクセスできます。 このプロパティの値にアクセスする方法の詳細については、「[デバイスのセットアップクラス SPCRP_Xxx のプロパティの取得](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-spcrp-xxx-properties)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

 






