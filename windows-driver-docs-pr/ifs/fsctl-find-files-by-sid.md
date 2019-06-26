---
title: FSCTL_FIND_FILES_BY_SID 制御コード
description: FSCTL\_検索\_ファイル\_BY\_SID 制御コード検索ディレクトリにファイルの作成者と所有者 matche SID を指定します。
ms.assetid: fe0953d3-a009-431b-b03b-5d827dc732a1
keywords:
- FSCTL_FIND_FILES_BY_SID 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_FIND_FILES_BY_SID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc53452329a57104721074f9a41697c2e9bb886c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365031"
---
# <a name="fsctlfindfilesbysid-control-code"></a>FSCTL\_検索\_ファイル\_BY\_SID 制御コード


FSCTL\_検索\_ファイル\_BY\_SID 制御コード検索ディレクトリにファイルの作成者と所有者 matche SID を指定します。

ミニフィルター ドライバーの呼び出しは、この操作を実行する[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)の次のパラメーターとファイル システム リダイレクター、および従来のファイル システム フィルター ドライバー呼び出し[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 検索するディレクトリのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 検索するディレクトリのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 FSCTL を使用して、\_検索\_ファイル\_BY\_この操作の SID。

<a href="" id="inputbuffer"></a>*InputBuffer*  
検索によって記述される入力バッファーへのポインター\_BY\_SID\_データ構造体。 検索\_BY\_SID\_データ構造は次のように定義されます。

```cpp
typedef struct {
  DWORD  ;
  SID  ;
} FIND_BY_SID_DATA, *PFIND_BY_SID_DATA;
```

**メンバー**

<a href="" id="restart"></a>**再起動**  
検索を再開するかどうかを示します。 このメンバーは、ルートから検索を開始できるように、最初の呼び出しで 1 に設定する必要があります。 後続の呼び出しの検索が停止した位置に再開されますので、このメンバーを 0 に設定する必要があります。

<a href="" id="sid-"></a>**sid**   
型の構造体[ **SID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_sid)作成者と所有者を指定します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
(バイト単位)、バッファーの長さ*InputBuffer*します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
クアッドで固定された検索の呼び出し元が割り当てた配列へのポインター\_BY\_SID\_各ファイルの完全修飾パス名を受け取る出力構造体。 検索\_BY\_SID\_出力の構造は次のように定義されます。

```cpp
typedef struct _FIND_BY_SID_OUTPUT {
  DWORD  ;
  DWORD  ;
  DWORD  ;
  WCHAR  [1];
} FIND_BY_SID_OUTPUT, *PFIND_BY_SID_OUTPUT;
```

**メンバー**

<a href="" id="nextentryoffset"></a>**NextEntryOffset**  
次のレコードにスキップする必要がありますバイト数。 ゼロの値は、最後のレコードであることを示します。

<a href="" id="fileindex-"></a>**FileIndex**   
ファイルのインデックス。

<a href="" id="filenamelength-"></a>**FileNameLength**   
(バイト単位)、ファイル名のサイズ。

<a href="" id="filename-"></a>**FileName**   
ファイル名を指定する null で終わる文字列。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指すバッファーに返されるデータのバイト単位のサイズ、 *OutputBuffer*パラメーター。

<a name="remarks"></a>注釈
-------

ときに[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)と[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)プロセス、 **FSCTL\_検索\_ファイル\_BY\_SID**制御コードは、これらのルーチンは、すべてのファイルと、ボリューム上のディレクトリを確認します。 この操作は、検索するディレクトリが非常に小さい場合でもボリュームでは、多くのファイルがある場合は低速可能性があります。

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_sid)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






