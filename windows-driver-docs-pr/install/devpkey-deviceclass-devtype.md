---
title: DEVPKEY_DeviceClass_DevType
description: DEVPKEY_DeviceClass_DevType
ms.assetid: 383f2b47-c0ee-49c2-851c-b18c98fd0303
keywords:
- DEVPKEY_DeviceClass_DevType デバイスとドライバーのインストール
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
ms.openlocfilehash: 1d1f7c3fb5c42bc49c71a878c69b10ad7067b5b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828876"
---
# <a name="devpkey_deviceclass_devtype"></a>DEVPKEY_DeviceClass_DevType


DEVPKEY_DeviceClass_DevType device プロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)の既定のデバイスの種類を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>プロパティアクセス</strong></p></td>
<td align="left"><p>デバイスセットアップクラスがインストールされた後のインストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_DEVTYPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

インストールアプリケーションがデバイスセットアップクラスをインストールするときに、DEVPKEY_DeviceClass_DevType の値を設定できます。 デバイスセットアップクラスをインストールし、このプロパティを設定する方法の詳細については、「 [**INF ClassInstall32」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)と、「特殊な*値-エントリ名*」に記載されているレジストリエントリ値 **(devicetype**に関する情報を参照してください。「 [**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」の「」を参照してください。

DEVPKEY_DeviceClass_DevType の値は、Wdm および Ntddk で定義されている FILE_DEVICE_Xxx 値の1つです。 デバイスの種類の詳細については、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)関数の *(devicetype*パラメーターを参照してください。

[**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出して、DEVPKEY_DeviceClass_DevType の値を取得できます。

Windows Server 2003 および Windows XP では、このプロパティはサポートされていますが、DEVPKEY_DeviceClass_DevType プロパティキーはサポートされていません。 以前のバージョンの Windows では、SPCRP_DEVTYPE 識別子を使用して、このプロパティの値にアクセスできます。 このプロパティの値にアクセスする方法の詳細については、「[デバイスセットアップクラスの取得 SPCRP_Xxx のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-spcrp-xxx-properties)」を参照してください。

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
<td align="left"><p>Header</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

 






