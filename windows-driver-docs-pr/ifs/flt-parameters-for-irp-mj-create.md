---
title: FLT_PARAMETERS irp_mj_create 用共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_作成。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- FLT_PARAMETERS irp_mj_create 用共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: d54dd95ae168e5b6245df0d63d2759e98d9614aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582269"
---
# <a name="fltparameters-for-irpmjcreate-union"></a>FLT\_IRP のパラメーター\_MJ\_共用体の作成


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は構造体[ **IRP\_MJ\_作成**](irp-mj-create.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIO_SECURITY_CONTEXT     SecurityContext;
    ULONG                    Options;
    USHORT POINTER_ALIGNMENT FileAttributes;
    USHORT                   ShareAccess;
    USHORT POINTER_ALIGNMENT EaLength;
    PVOID                    EaBuffer;
    LARGE_INTEGER            AllocationSize;
  } Create;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**作成します。**  
次のメンバーを含む構造体。

**SecurityContext**  
SecurityContext-&gt;AccessState

ポインター、 [**アクセス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff538840)オブジェクトのサブジェクトのコンテキストを含んでいる構造体のアクセスが許可の種類、および残りの必要なアクセスの種類。

SecurityContext-&gt;DesiredAccess

[**アクセス\_マスク**](https://msdn.microsoft.com/library/windows/hardware/ff540466)ファイルに対して要求されたアクセス権を指定する構造体。 詳細については、、 *DesiredAccess*パラメーターを[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)を参照してください。

**[オプション]**  
作成またはファイルが既に存在する場合に実行されるアクションと同様に、ファイルを開くときに適用されるオプションを指定するフラグのビットマスク。 このメンバーの下位 24 ビットに対応しています、 *CreateOptions*パラメーターを[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)します。 上位の 8 ビットに対応しています、 *CreateDisposition*パラメーターを**FltCreateFile**します。

**FileAttributes**  
属性の作成またはファイルを開く際に適用するビット マスク。 詳細については、、 *FileAttributes*パラメーターを[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)を参照してください。

**ShareAccess**  
ファイルに、要求は共有アクセス権限のビットマスクです。 このパラメーターが 0 の場合は、排他的アクセスが要求されています。 詳細については、、 *ShareAccess*パラメーターを[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)を参照してください。

**EaLength**  
バッファーのバイト単位の長さを**EaBuffer**へのポインターします。 詳細については、、 *EaLength*パラメーターを[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)を参照してください。

**EaBuffer**  
呼び出し元が指定へのポインター [**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)-に適用される拡張属性 (EA) の情報を格納している構造化されたバッファーファイルです。 詳細については、、 *EaBuffer*パラメーターを[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)を参照してください。

**AllocationSize**  
必要に応じて、ファイルのバイト単位で初期割り当てサイズを指定します。 0 以外の値及ぼしませんしない限り、ファイルが作成されている、上書き、または置き換えできます。 詳細については、、 *AllocationSize*パラメーターを[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)を参照してください。

<a name="remarks"></a>コメント
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)用の構造、 [ **IRP\_MJ\_作成**](irp-mj-create.md)操作コールバック データによって表される ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)構造体。

IRP\_MJ\_作成は IRP ベースの操作。

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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**アクセス\_マスク**](https://msdn.microsoft.com/library/windows/hardware/ff540466)

[**アクセス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff538840)

[**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

 

 






