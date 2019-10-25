---
title: IRP_MJ_QUERY_SECURITY 共用体の FLT_PARAMETERS
description: FLT\_IO\_パラメーター\_操作のブロック構造の MajorFunction フィールドが IRP\_MJ\_クエリ\_セキュリティである場合に使用される共用体コンポーネント。
ms.assetid: 7707fec2-9fe8-40f6-9f34-f43403551440
keywords:
- IRP_MJ_QUERY_SECURITY union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: fea2cb7033b12ba9ae37dc1cdb6c10447eb111ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841358"
---
# <a name="flt_parameters-for-irp_mj_query_security-union"></a>IRP\_MJ\_クエリ\_セキュリティ共用体の FLT\_パラメーター


[**FLT\_IO\_パラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作のブロック構造の**MajorFunction**フィールドが[**IRP\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)である場合に使用される共用体コンポーネント。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    SECURITY_INFORMATION    SecurityInformation;
    ULONG POINTER_ALIGNMENT Length;
    PVOID                   SecurityBuffer;
    PDML                    MdlAddress;
  } QuerySecurity;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**QuerySecurity**  
次のメンバーを含む構造体。

**SecurityInformation**  
照会するセキュリティ情報を指定する、呼び出し元が指定した[**セキュリティ\_情報**](security-information.md)の値へのポインター。 次のいずれかです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation の値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者識別子が照会されています。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリグループ識別子が照会されています。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの随意アクセス制御リスト (DACL) を照会しています。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのシステム ACL (SACL) を照会しています。 ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
</tbody>
</table>

 

**長さ**  
**Securitybuffer**が指すバッファーの長さ (バイト単位)。

**SecurityBuffer**  
指定したオブジェクトのセキュリティ記述子のコピーを受け取る、呼び出し元から提供される出力バッファーへのポインター。 呼び出しプロセスには、オブジェクトのセキュリティステータスの指定した側面を表示する権限が必要です。 [**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))の構造体は、自己相対形式で返されます。

**MdlAddress**  
**Securitybuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

<a name="remarks"></a>注釈
-------

[**Irp\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータによって表される、irp ベースのクエリ-セキュリティ情報操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、 [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

Windows XP 以降では、FLT\_IO\_\_パラメーターの**Targetfileobject**メンバーが名前付きデータストリームを表すことができます。 名前付きデータストリームの詳細については、「[**ファイル\_ストリームの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)」を参照してください。

IRP\_MJ\_クエリ\_セキュリティは、IRP ベースの操作です。

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


[**ファイル\_ストリームの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)

[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**セキュリティ\_情報**](security-information.md)

 

 






