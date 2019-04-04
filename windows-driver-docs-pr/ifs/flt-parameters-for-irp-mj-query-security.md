---
title: FLT_PARAMETERS IRP_MJ_QUERY_SECURITY 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_クエリ\_セキュリティ。
ms.assetid: 7707fec2-9fe8-40f6-9f34-f43403551440
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_SECURITY 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 73f22e34f84a446b3e922a3568e18de85cfcba25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531295"
---
# <a name="fltparameters-for-irpmjquerysecurity-union"></a>FLT\_IRP のパラメーター\_MJ\_クエリ\_セキュリティ共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)します。

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
呼び出し元が指定へのポインター [**セキュリティ\_情報**](security-information.md)クエリを実行するセキュリティ情報を指定する値。 次のいずれかです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation 値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>照会されるオブジェクトの所有者の識別子。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>照会されるオブジェクトのプライマリ グループ id。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>照会されるオブジェクトの随意アクセス制御リスト (DACL)。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>照会されるオブジェクトのシステム ACL (SACL)。 ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
</tbody>
</table>

 

**長さ**  
バッファーのバイト単位の長さを**SecurityBuffer**を指します。

**SecurityBuffer**  
指定したオブジェクトのセキュリティ記述子のコピーを受け取る呼び出し元が指定の出力バッファーへのポインター。 呼び出し元のプロセスを指定したオブジェクトのセキュリティ状態の側面を表示する権限が必要です。 [**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)構造が自己相対形式で返されます。

**MdlAddress**  
バッファーを記述したメモリ記述子一覧 (MDL) のアドレスを**SecurityBuffer**を指します。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の構造体[ **IRP\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)操作にコールバック データによって表される IRP ベースのセキュリティ情報の照会操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620))構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)構造体。

Windows xp 以降、オブジェクトを**TargetFileObject** 、FLT のメンバー\_IO\_パラメーター\_ブロック構造のポイントには、名前付きのデータ ストリームを表すことができます。 名前付きのデータ ストリームの詳細については、[**ファイル\_ストリーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540364)を参照してください。

IRP\_MJ\_クエリ\_セキュリティは IRP ベースの操作。

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


[**ファイル\_ストリーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540364)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_QUERY\_SECURITY**](irp-mj-query-security.md)

[**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)

[**セキュリティ\_情報**](security-information.md)

 

 






