---
title: FLT_PARAMETERS IRP_MJ_PNP 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_PNP します。
ms.assetid: d3ce893b-f113-4c50-8f52-30c7ced25ae0
keywords:
- FLT_PARAMETERS IRP_MJ_PNP 共用体インストール可能なファイル システム ドライバー
- FLT_PARAMETERS union インストール可能なファイル システム ドライバー
- PFLT_PARAMETERS 共用体ポインター インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: b2de4b0995870523145a3df721fa0d3cc3a3c0a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353805"
---
# <a name="fltparameters-for-irpmjpnp-union"></a>FLT\_IRP のパラメーター\_MJ\_PNP 共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)します。

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

**Pnp**  
**StartDevice**  
IRP に使用される共用体のコンポーネント\_MN\_開始\_デバイス操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)します。

**QueryDeviceRelations**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_デバイス\_リレーション操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)します。

**QueryInterface**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_インターフェイス操作です。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)します。

**DeviceCapabilities**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_機能操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)します。

**FilterResourceRequirements**  
IRP に使用される共用体のコンポーネント\_MN\_フィルター\_リソース\_要件操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください[ **IRP\_MN\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements).

**ReadWriteConfig**  
IRP に使用される共用体のコンポーネント\_MN\_読み取り\_CONFIG および IRP\_MN\_書き込み\_構成操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください[ **IRP\_MN\_読み取り\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)と[ 。**IRP\_MN\_書き込み\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)します。

**SetLock**  
IRP に使用される共用体のコンポーネント\_MN\_設定\_ロック操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_設定\_ロック**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)します。

**QueryId**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_操作の ID。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)します。

**QueryDeviceText**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_デバイス\_テキスト操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_デバイス\_テキスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)します。

**UsageNotification**  
IRP に使用される共用体のコンポーネント\_MN\_デバイス\_使用状況\_通知操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください[ **IRP\_MN\_デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification) .

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)の構造体[ **IRP\_MJ\_PNP** ](irp-mj-pnp.md)操作コールバック データによって表される IRP ベース プラグ アンド プレイ (PnP) 操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体。

IRP\_MJ\_PNP 操作は IRP ベース操作。

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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_PNP (WDK カーネル モード ドライバーのアーキテクチャのリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP\_MN\_デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)

[**IRP\_MN\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)

[**IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

[**IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)

[**IRP\_MN\_QUERY\_DEVICE\_TEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)

[**IRP\_MN\_QUERY\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)

[**IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)

[**IRP\_MN\_READ\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)

[**IRP\_MN\_SET\_LOCK**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)

[**IRP\_MN\_START\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

[**IRP\_MN\_WRITE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)

 

 






