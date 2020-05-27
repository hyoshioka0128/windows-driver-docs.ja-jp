---
title: IRP_MJ_NETWORK_QUERY_OPEN 共用体の FLT_PARAMETERS
description: '\_ \_ 操作の FLT IO パラメーターブロック構造の MajorFunction フィールド \_ が IRP \_ MJ \_ NETWORK QUERY \_ OPEN \_ の場合は、次の共用体コンポーネントが使用されます。'
ms.assetid: bafe015c-a747-4d18-95d5-adad2ad1570b
keywords:
- IRP_MJ_NETWORK_QUERY_OPEN ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- PFLT_PARAMETERS 共用体ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: ced59d60ae17f5d1a7e1c1db0338bfc1a2a13189
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851964"
---
# <a name="flt_parameters-for-irp_mj_network_query_open-union"></a>FLT \_ PARAMETERS IRP \_ MJ \_ NETWORK \_ QUERY \_ OPEN union


操作の[**FLT \_ IO \_ パラメーター \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが IRP \_ MJ NETWORK QUERY OPEN の場合は、次の共用体コンポーネントが使用され \_ \_ \_ ます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIRP                           Irp;
    PFILE_NETWORK_OPEN_INFORMATION NetworkInformation;
  } NetworkQueryOpen;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**NetworkQueryOpen**  
次のメンバーを含む構造体。

**Irp**  
このオープン操作を表す create IRP へのポインター。 この IRP は、一般的な open/create コードにファイルシステムによって使用されますが、実際には完了していません。

**NetworkInformation**  
ファイルネットワークへのポインターは、ファイルに関する要求された情報を受け取るために、 [** \_ \_ \_ 情報を開い**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)ています。

<a name="remarks"></a>コメント
-------

IRP MJ NETWORK QUERY open 操作の[**FLT \_ parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、 \_ \_ \_ \_ コールバックデータ ([**FLT \_ callback \_ Data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される networkqueryopen 操作のパラメーターが含まれています。 **FLT \_ PARAMETERS**構造体は、 [**FLT \_ IO \_ パラメーター \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

> [!NOTE]
> IRP MJ NETWORK QUERY OPEN に関連付けられているファイルオブジェクト \_ \_ は、 \_ \_ スタックベースのオブジェクトです。
NetworkQueryOpen コールバックに登録されているフィルターは、このオブジェクトを参照できません。 つまり、このスタックベースのファイルオブジェクトでは、ObReferenceObject または ObDereferenceObject を呼び出さないでください。 また、オブジェクトへのポインターを保存しないでください。

 

IRP \_ MJ \_ NETWORK \_ QUERY \_ OPEN は、高速な i/o 操作です。 これは、fa/Oqueryopen (Fa/Faoquerynetworkopeninfo ではない) 操作に相当します。 この操作を行うには、フィルターを登録する必要があります。

<a name="requirements"></a>必要条件
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


[**ファイル \_ ネットワークの \_ オープン \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**FLT \_ CALLBACK \_ データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ パラメーター \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ の \_ \_ 操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT \_ IS \_ FS \_ FILTER \_ 操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT \_ は \_ IRP \_ 操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT \_ パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**IRP \_ MJ の \_ クエリ \_ 情報**](irp-mj-query-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






