---
title: IRP_MJ_PNP 共用体の FLT_PARAMETERS
description: 操作の FLT\_IO\_パラメーター\_ブロック構造の MajorFunction フィールドが IRP\_MJ\_PNP である場合に使用される共用体コンポーネント。
ms.assetid: d3ce893b-f113-4c50-8f52-30c7ced25ae0
keywords:
- IRP_MJ_PNP union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
- FLT_PARAMETERS union にインストール可能なファイルシステムドライバー
- PFLT_PARAMETERS union ポインターのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3616ed735b800711ea85c3581e016ed3ed589391
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841368"
---
# <a name="flt_parameters-for-irp_mj_pnp-union"></a>IRP\_MJ\_PNP 共用体の FLT\_パラメーター


操作の[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが[**IRP\_MJ\_PNP**](irp-mj-pnp.md)である場合に使用される共用体コンポーネント。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct  StartDevice;
    struct  QueryDeviceRelations;
    struct  QueryInterface;
    struct  DeviceCapabilities;
    struct  FilterResourceRequirements;
    struct  ReadWriteConfig;
    struct  SetLock;
    struct  QueryId;
    struct  QueryDeviceText;
    struct  UsageNotification;
  } Pnp;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**全て**  
**StartDevice**  
IRP\_に使用されるユニオンコンポーネントで\_デバイス操作を開始\_。 この操作のパラメーターの詳細については、 [ **\_デバイスを起動\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)には、IRP\_の参照エントリを参照してください。

**QueryDeviceRelations**  
IRP\_\_クエリ\_デバイス\_リレーション操作に使用される共用体コンポーネント。 この操作のパラメーターの詳細については、「 [**IRP\_\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)」の参照エントリを参照してください。

**QueryInterface**  
IRP\_\_クエリ\_インターフェイス操作に使用される共用体コンポーネントです。 この操作のパラメーターの詳細については、「 [**IRP\_\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)の参照エントリ」を参照してください。

**DeviceCapabilities**  
IRP\_\_クエリ\_機能操作に使用される共用体コンポーネントです。 この操作のパラメーターの詳細については、次を参照してください。 [**IRP\_は、\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)の参照エントリです。

**FilterResourceRequirements**  
IRP\_\_フィルター\_リソース\_要件操作に使用される共用体コンポーネント。 この操作のパラメーターの詳細については、「 [**IRP\_\_フィルター\_リソース\_の要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)」の参照エントリを参照してください。

**ReadWriteConfig**  
IRP\_に使用される共用体コンポーネント。\_読み取り\_構成と IRP\_、\_構成操作を書き込むことができます。 この操作のパラメーターの詳細については、次を参照してください。 [**irp\_は、\_読み取り\_構成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)と\_irp の参照エントリ[ **\_書き込み\_構成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)ます。

**SetLock**  
IRP\_\_設定\_ロック操作に使用される共用体コンポーネント。 この操作のパラメーターの詳細については、次を参照してください。 [**IRP\_が\_ロック\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)されています。

**QueryId**  
IRP\_\_クエリ\_ID 操作に使用される共用体コンポーネントです。 この操作のパラメーターの詳細については、「 [**IRP\_\_クエリ\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)の参照エントリ」を参照してください。

**QueryDeviceText**  
IRP\_\_クエリ\_デバイス\_テキスト操作に使用される共用体コンポーネント。 この操作のパラメーターの詳細については、「 [**IRP\_\_クエリ\_デバイス\_テキスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)」の参照エントリを参照してください。

**UsageNotification**  
IRP\_\_デバイス\_使用状況\_通知操作に使用される共用体コンポーネント。 この操作のパラメーターの詳細については、「 [**IRP\_\_デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)」の参照エントリを参照してください。

<a name="remarks"></a>注釈
-------

[**Irp\_MJ\_の pnp**](irp-mj-pnp.md)操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) によって表される irp ベースプラグアンドプレイ (pnp) 操作のパラメーターが含まれています。データ. これは、 [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

IRP\_MJ\_PNP 操作は、IRP ベースの操作です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_PNP (WDK カーネルモードドライバーアーキテクチャリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP\_\_デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)

[**IRP\_\_フィルター\_リソース\_の要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)

[**IRP\_\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

[**IRP\_\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)

[**IRP\_\_クエリ\_デバイス\_テキスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)

[**IRP\_\_クエリ\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)

[**IRP\_\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)

[**IRP\_\_読み取り\_構成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)

[**IRP\_\_設定\_ロック**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)

[ **\_デバイスを起動\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

[**IRP\_\_書き込み\_構成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)

 

 






