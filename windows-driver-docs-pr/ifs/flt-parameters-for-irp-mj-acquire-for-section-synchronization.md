---
title: FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体
description: 次の共用体のコンポーネントは、操作の FLT_IO_PARAMETER_BLOCK 構造の MajorFunction フィールドは IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION ときに使用されます。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: af83db238aa83ab081c913ce0f81de390e631495
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365076"
---
# <a name="fltparameters-for-irpmjacquireforsectionsynchronization-union"></a>FLT\_IRP のパラメーター\_MJ\_ACQUIRE\_の\_セクション\_同期共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は IRP を構造体\_MJ\_ACQUIRE\_の\_セクション\_同期します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    FS_FILTER_SECTION_SYNC_TYPE SyncType;
    ULONG POINTER_ALIGNMENT     PageProtection;
    PFS_FILTER_SECTION_SYNC_OUTPUT OutputInformation;
  } AcquireForSectionSynchronization;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**SyncType**  
* 同期のセクションの要求の種類を指定します。 このパラメーターは、2 つの列挙値のいずれかを指定する必要があります。
  * **SyncTypeCreateSection**
  * **SyncTypeOther**

**PageProtection**  
* セクションの要求されたページ保護の種類を指定します。 場合は 0 にする必要があります**SyncType** SyncTypeOther です。 それ以外の場合、次のいずれかのフラグ、可能性があるページと組み合わせて\_NOCACHE:

  * ページ\_読み取り専用

  * ページ\_READWRITE

  * ページ\_WRITECOPY

  * ページ\_EXECUTE

**OutputInformation**
*  A [ **FS_FILTER_SECTION_SYNC_OUTPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fs_filter_section_sync_output)構造が作成されているセクションの属性を説明する情報を指定します。

## <a name="remarks"></a>注釈


[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_ACQUIRE\_の\_セクション\_同期操作のパラメーターを格納する、 **AcquireForSectionSynchronization**コールバック データによって表される操作 ([**FLT\_コールバック\_データ** ](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_ACQUIRE\_の\_セクション\_同期は、ファイル システム (FSFilter) のコールバック操作。

場合の列挙値、 **SyncType**に設定されているメンバー **SyncTypeOther** (ゼロ)、ファイル システム ミニフィルターまたはレガシ フィルター ドライバーをこの操作に失敗することはできません。 場合**SyncType**に設定されている**SyncTypeCreateSection**、ファイル システム ミニフィルターまたはレガシ フィルター ドライバーの状態で失敗が許可される\_不十分\_リソース エラー場合セクションを作成するための十分なメモリがありません。

FSFilter コールバック操作の詳細については、参照のエントリを参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)します。

## <a name="requirements"></a>必要条件


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
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

[**FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)

 

 






