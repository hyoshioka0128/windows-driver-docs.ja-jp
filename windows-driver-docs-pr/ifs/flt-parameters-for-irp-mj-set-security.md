---
title: FLT_PARAMETERS IRP_MJ_SET_SECURITY 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_設定\_セキュリティ。
ms.assetid: 9006ef50-bd2e-4c75-8c6b-8bb777122a75
keywords:
- FLT_PARAMETERS IRP_MJ_SET_SECURITY 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 0e3a3d4c3f8b35612494d8f8cf1f40ac0c27c18d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530713"
---
# <a name="fltparameters-for-irpmjsetsecurity-union"></a>FLT\_IRP のパラメーター\_MJ\_設定\_セキュリティ共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_設定\_セキュリティ**](irp-mj-set-security.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    SECURITY_INFORMATION SecurityInformation;
    PSECURITY_DESCRIPTOR SecurityDescriptor;
  } SetSecurity;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**SetSecurity**  
次のメンバーを含む構造体。

**SecurityInformation**  
ポインターを[**セキュリティ\_情報**](security-information.md)セキュリティ情報を指定する値は、セキュリティ記述子に設定します。 この値は、次のいずれかを指定できます。

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
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの随意アクセス制御リスト (DACL) が設定されています。 対する WRITE_DAC アクセス許可が必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリ グループ id が設定されています。 WRITE_OWNER アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者の識別子が設定されています。 WRITE_OWNER アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのシステム ACL (SACL) が設定されています。 ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
</tbody>
</table>

 

**SecurityDescriptor**  
ポインターを[**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)オブジェクトに割り当てられるセキュリティ情報の値を含む構造体。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の構造体[ **IRP\_MJ\_設定\_セキュリティ**](irp-mj-set-security.md)操作にはコールバック データによって表されるセットの情報セキュリティ操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620))構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_設定\_セキュリティは IRP ベースの操作。

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


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_SET\_SECURITY**](irp-mj-set-security.md)

[**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)

[**セキュリティ\_情報**](security-information.md)

 

 






