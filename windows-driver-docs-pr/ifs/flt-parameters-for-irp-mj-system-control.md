---
title: FLT_PARAMETERS IRP_MJ_SYSTEM_CONTROL 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_システム\_コントロール。
ms.assetid: 6f1c34b2-1c79-4372-8b94-afe4b50294d5
keywords:
- FLT_PARAMETERS IRP_MJ_SYSTEM_CONTROL 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 6a00b21b822ad710cf165e6c08fbf3adbc6e2fdf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579642"
---
# <a name="fltparameters-for-irpmjsystemcontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_システム\_コントロール共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が IRP\_MJ\_システム\_コントロール。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG_PTR ProviderId;
    PVOID     DataPath;
    ULONG     BufferSize;
    PVOID     Buffer;
  } WMI;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**WMI**  
次のメンバーを含む構造体。

**ProviderId**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

**データパス**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

**BufferSize**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

**Buffer**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

<a name="remarks"></a>コメント
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_システム\_管理操作には、システム コントロールの操作のパラメーターが含まれています。コールバック データによって表される ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP の意味\_MJ\_システム\_制御パラメーターは、マイナー関数コードによって異なります。 (を参照してください、 **MinorFunction**のメンバー、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)構造です)。詳細については、次の小さな関数のコードに対して参照エントリを参照してください。

[**IRP\_MN\_変更\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff550831)

[**IRP\_MN\_変更\_単一\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff550836)

[**IRP\_MN\_DISABLE\_COLLECTION**](https://msdn.microsoft.com/library/windows/hardware/ff550848)

[**IRP\_MN\_を無効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550851)

[**IRP\_MN\_ENABLE\_COLLECTION**](https://msdn.microsoft.com/library/windows/hardware/ff550857)

[**IRP\_MN\_を有効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550859)

[**IRP\_MN\_EXECUTE\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff550868)

[**IRP\_MN\_クエリ\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551650)

[**IRP\_MN\_クエリ\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff551718)

[**IRP\_MN\_REGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551731)

[**IRP\_MN\_REGINFO\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff551734)

IRP\_MJ\_システム\_コントロールが IRP ベースの操作。

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


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MN\_変更\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff550831)

[**IRP\_MN\_変更\_単一\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff550836)

[**IRP\_MN\_DISABLE\_COLLECTION**](https://msdn.microsoft.com/library/windows/hardware/ff550848)

[**IRP\_MN\_を無効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550851)

[**IRP\_MN\_ENABLE\_COLLECTION**](https://msdn.microsoft.com/library/windows/hardware/ff550857)

[**IRP\_MN\_を有効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550859)

[**IRP\_MN\_EXECUTE\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff550868)

[**IRP\_MN\_クエリ\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551650)

[**IRP\_MN\_クエリ\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff551718)

[**IRP\_MN\_REGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551731)

[**IRP\_MN\_REGINFO\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff551734)

 

 






