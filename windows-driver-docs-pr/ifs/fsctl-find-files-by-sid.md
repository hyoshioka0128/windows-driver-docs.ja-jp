---
title: FSCTL_FIND_FILES_BY_SID 制御コード
description: '\_SID 制御コードによって\_された\_ファイルを検索\_は、指定した SID に一致するクリエーターと所有者があるファイルをディレクトリで検索します。'
ms.assetid: fe0953d3-a009-431b-b03b-5d827dc732a1
keywords:
- FSCTL_FIND_FILES_BY_SID 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_FIND_FILES_BY_SID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64fe5299f09585574e7effbdbacd272ecd1f677f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841311"
---
# <a name="fsctl_find_files_by_sid-control-code"></a>FSCTL\_\_SID 制御コードによって\_\_ファイルを検索する


\_SID 制御コードによって\_された\_ファイルを検索\_は、指定した SID に一致するクリエーターと所有者があるファイルをディレクトリで検索します。

この操作を実行するには、ミニフィルタードライバーは、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)を呼び出します。ファイルシステム、リダイレクター、およびレガシファイルシステムフィルタードライバーは、次のパラメーターを使用して[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 検索するディレクトリのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 検索するディレクトリのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 FSCTL を使用して、この操作の\_SID によって\_ファイルを検索\_\_します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
\_SID\_データ構造によって検索\_によって記述された入力バッファーへのポインター。 \_SID\_データ構造による検索\_は、次のように定義されています。

```cpp
typedef struct {
  DWORD  ;
  SID  ;
} FIND_BY_SID_DATA, *PFIND_BY_SID_DATA;
```

**属する**

<a href="" id="restart"></a>**一度**  
検索を再開するかどうかを示します。 最初の呼び出しでこのメンバーを1に設定して、検索がルートから開始されるようにする必要があります。 後続の呼び出しでは、このメンバーを0に設定して、検索が停止した時点で再開されるようにする必要があります。

<a href="" id="sid-"></a>**Sid**   
作成者と所有者を指定する[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)型の構造体。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*のバッファーの長さ (バイト単位)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
各ファイルの完全修飾パス名を受け取る\_SID\_出力構造体を使用して、クワッドアラインされた検索\_の呼び出し元が割り当てた配列へのポインター。 FIND\_BY\_SID\_の出力構造は次のように定義されています。

```cpp
typedef struct _FIND_BY_SID_OUTPUT {
  DWORD  ;
  DWORD  ;
  DWORD  ;
  WCHAR  [1];
} FIND_BY_SID_OUTPUT, *PFIND_BY_SID_OUTPUT;
```

**属する**

<a href="" id="nextentryoffset"></a>**NextEntryOffset**  
次のレコードに到達するためにスキップする必要があるバイト数。 値が0の場合は、これが最後のレコードであることを示します。

<a href="" id="fileindex-"></a>**Fileindex**   
ファイルのインデックス。

<a href="" id="filenamelength-"></a>**FileNameLength**   
ファイル名のサイズ (バイト単位)。

<a href="" id="filename-"></a>**ファイル名**   
ファイル名を指定する null で終わる文字列。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターによって示されるバッファーで返されるデータのサイズ (バイト単位)。

<a name="remarks"></a>注釈
-------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)と[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)が **\_SID 制御コードによって\_\_ファイルを検索\_** 場合、これらのルーチンはボリューム上のすべてのファイルとディレクトリをチェックします。 この操作は、検索するディレクトリが非常に小さい場合でも、ボリュームに多数のファイルがあると、処理が遅くなることがあります。

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






