---
title: FLT_PARAMETERS IRP_MJ_NETWORK_QUERY_OPEN 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_ネットワーク\_クエリ\_開きます。
ms.assetid: bafe015c-a747-4d18-95d5-adad2ad1570b
keywords:
- FLT_PARAMETERS IRP_MJ_NETWORK_QUERY_OPEN 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: a7ed19b2c5a58fd1dba80d11b37c958640c01763
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353808"
---
# <a name="fltparameters-for-irpmjnetworkqueryopen-union"></a>FLT\_IRP のパラメーター\_MJ\_ネットワーク\_クエリ\_オープン共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作は IRP を構造体\_MJ\_ネットワーク\_クエリ\_開きます。

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

<a name="members"></a>Members
-------

**NetworkQueryOpen**  
次のメンバーを含む構造体。

**Irp**  
このオープン操作を表す IRP の作成へのポインター。 この IRP が開くか作成の一般的なコードに、ファイル システムで使用するが実際に完了しました。

**NetworkInformation**  
ポインターを[**ファイル\_ネットワーク\_オープン\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)-要求されたファイルに関する情報を受信するバッファーを構造化します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP の構造\_MJ\_ネットワーク\_クエリ\_オープン操作にはパラメーターが含まれています、コールバック データによって表される NetworkQueryOpen 操作 ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 **FLT\_パラメーター**に構造体が含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体。

&gt; \[!注\]IRP に関連付けられているファイル オブジェクト\_MJ\_ネットワーク\_クエリ\_なスタック ベースのオブジェクトのファイルを開く。
&gt;フィルターを NetworkQueryOpen コールバックの登録は、このオブジェクトを参照する必要があります。 つまり、呼び出さないでください ObReferenceObject または ObDereferenceObject このスタック ベースのファイル オブジェクト。 また、保存しないポインター オブジェクト。

 

IRP\_MJ\_ネットワーク\_クエリ\_な高速な I/O 操作のファイルを開く。 FastIoQueryOpen (FastIoQueryNetworkOpenInfo ではない) 操作に相当することをお勧めします。 フィルターは、この操作に登録する必要があります。

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


[**FILE\_NETWORK\_OPEN\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






