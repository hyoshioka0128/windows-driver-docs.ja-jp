---
title: IRP_MJ_NETWORK_QUERY_OPEN 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーター\_のブロック構造の MajorFunction フィールドが、操作に対する IRP\_MJ\_ネットワーク\_クエリ\_開いている場合に使用されます。
ms.assetid: bafe015c-a747-4d18-95d5-adad2ad1570b
keywords:
- IRP_MJ_NETWORK_QUERY_OPEN union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: d7e9242c16bd2ad36fb110cb98f97914bde3f829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841375"
---
# <a name="flt_parameters-for-irp_mj_network_query_open-union"></a>IRP\_MJ\_NETWORK\_QUERY\_OPEN union の FLT\_パラメーター


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーター\_のブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが、操作に対する IRP\_MJ\_ネットワーク\_クエリ\_開いている場合に使用されます。

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
このオープン操作を表す create IRP へのポインター。 この IRP は、一般的な open/create コードにファイルシステムによって使用されますが、実際には完了していません。

**System.net.networkinformation**  
ファイル\_ネットワークへのポインター [ **\_\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)構造化バッファーを開いて、ファイルに関する要求された情報を受け取ります。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_NETWORK\_QUERY\_OPEN 操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ (FLT\_callback によって表される NetworkQueryOpen 操作のパラメーターが含まれてい[ **\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 **FLT\_PARAMETERS**構造体は、 [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

&gt; \[!IRP\_MJ\_NETWORK\_QUERY\_OPEN に関連付けられているファイルオブジェクトは、スタックベースのオブジェクトであることに注意してください\]。
NetworkQueryOpen コールバックに登録されているフィルターでは、このオブジェクトを参照しないように &gt;必要があります。 つまり、このスタックベースのファイルオブジェクトでは、ObReferenceObject または ObDereferenceObject を呼び出さないでください。 また、オブジェクトへのポインターを保存しないでください。

 

IRP\_MJ\_ネットワーク\_クエリ\_OPEN は高速 i/o 操作です。 これは、fa/Oqueryopen (Fa/Faoquerynetworkopeninfo ではない) 操作に相当します。 この操作を行うには、フィルターを登録する必要があります。

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


[**ファイル\_ネットワーク\_\_情報を開く**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






