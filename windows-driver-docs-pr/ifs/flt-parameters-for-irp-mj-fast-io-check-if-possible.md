---
title: FLT_PARAMETERS IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_高速\_IO\_確認\_場合\_可能です。
ms.assetid: 1de62b03-4073-40d6-9094-609431e19e5b
keywords:
- FLT_PARAMETERS IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 168968665c215adcb7a540b12f2564d567d6ffad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365004"
---
# <a name="fltparameters-for-irpmjfastiocheckifpossible-union"></a>FLT\_IRP のパラメーター\_MJ\_高速\_IO\_確認\_場合\_可能な共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は IRP を構造体\_MJ\_高速\_IO\_確認\_場合\_可能です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER             FileOffset;
    ULONG                     Length;
    ULONG POINTER_ALIGNMENT   LockKey;
    BOOLEAN POINTER_ALIGNMENT CheckForReadOperation;
  } FastIoCheckIfPossible;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**FastIoCheckIfPossible**  
次のメンバーを含む構造体。

**FileOffset**  
キャッシュされたファイル内のバイト オフセットを開始しています。

**長さ**  
(バイト単位) の長さ、データを読み取りまたは書き込み。

**LockKey**  
ターゲット ファイルのバイト範囲ロックに関連付けられているキーの値。 読み取りまたは書き込みする範囲と重複またはファイル内で排他的にロックされている範囲のサブ範囲が、このパラメーターはその共有ロックのキーである必要があります。 呼び出し元のスレッドの親プロセスが、共有ロックを保持する必要があります。それ以外の場合、このパラメーターは無視されます。

**CheckForReadOperation**  
この操作は、読み取りを確認するか、操作を記述するかどうかを指定します。 設定されている**TRUE**読み取り操作と**FALSE**書き込み操作の。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_高速\_IO\_確認\_場合\_可能な操作のパラメーターを格納する、 **FastIoCheckIfPossible**コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_高速\_IO\_確認\_場合\_可能な限り高速な I/O 操作は、します。

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

[**FsRtlAreThereCurrentFileLocks**](https://msdn.microsoft.com/library/windows/hardware/ff545697)

[**FsRtlCopyRead**](https://msdn.microsoft.com/library/windows/hardware/ff545791)

[**FsRtlCopyWrite**](https://msdn.microsoft.com/library/windows/hardware/ff545797)

 

 






