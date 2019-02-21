---
title: FLT_PARAMETERS IRP_MJ_RELEASE_FOR_MOD_WRITE 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_リリース\_の\_MOD\_を記述します。
ms.assetid: 66b43d77-5e46-48b6-b86c-4ed21959ab49
keywords:
- FLT_PARAMETERS IRP_MJ_RELEASE_FOR_MOD_WRITE 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 9d681e21f89da8b0891b119e50b6d679958b51a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535998"
---
# <a name="fltparameters-for-irpmjreleaseformodwrite-union"></a>FLT\_IRP のパラメーター\_MJ\_リリース\_の\_MOD\_書き込み共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は IRP を構造体\_MJ\_リリース\_の\_MOD\_を記述します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PERESOURCE ResourceToRelease;
  } ReleaseForModifiedPageWriter;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**ReleaseForModifiedPageWriter**  
次のメンバーを含む構造体。

**ResourceToRelease**  
解放されるリソースへのポインター。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_リリース\_の\_MOD\_書き込み操作が含まれていますパラメーターを**ReleaseForModifiedPageWriter**コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620))構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_リリース\_の\_MOD\_書き込みは、ファイル システム (FSFilter) のコールバック操作。

FSFilter コールバック操作の詳細については、参照のエントリを参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)します。

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

[**FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)

 

 






