---
title: FSCTL_GET_RETRIEVAL_POINTERS 制御コード
description: FSCTL\_GET\_取得\_ポインター制御コードは、特定のファイルのディスク上の割り当てと場所を記述する可変サイズのデータ構造を取得します。
ms.assetid: d77790c8-9fe6-4b36-995e-40a7ea54c18a
keywords:
- FSCTL_GET_RETRIEVAL_POINTERS 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_GET_RETRIEVAL_POINTERS
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9f6bb4e809aea3b53dfefa28261ac67ea20602
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841303"
---
# <a name="fsctl_get_retrieval_pointers-control-code"></a>FSCTL\_取得\_取得\_ポインター制御コード


**FSCTL\_GET\_取得\_ポインター**制御コードは、特定のファイルのディスク上の割り当てと場所を記述する可変サイズのデータ構造を取得します。 構造体は、仮想クラスター番号 (VCN、ファイル/ストリーム領域内のオフセット)、および論理クラスター番号 (LCN、ボリューム領域内のオフセット) との間のマッピングを記述します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

再解析ポイントおよび FSCTL\_GET\_取得\_ポインターコントロールコードの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**パラメーター**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 FSCTL\_GET\_取得\_ポインターがマッピングを取得する代替ストリーム、ファイル、またはディレクトリのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 FSCTL\_GET\_取得\_ポインターがマッピングを取得する代替ストリーム、ファイル、またはディレクトリのファイルハンドル。 *FileHandle*の値がボリューム全体のハンドルである場合、ルーチンは、無効なクラスターファイルの vcns とエクステントのマップを返します。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作を行うには、FSCTL\_使用して\_取得\_ポインターを取得してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
代替ストリーム、ファイル、またはディレクトリの先頭をマークする仮想クラスター番号 (VCN) を示す、開始\_VCN\_入力\_バッファー構造体へのポインター。 開始\_の VCN\_入力\_バッファー構造は、次のように定義されています。

```cpp
typedef struct {
  LARGE_INTEGER  ;
} STARTING_VCN_INPUT_BUFFER, *PSTARTING_VCN_INPUT_BUFFER;
```

**属する**

<a href="" id="startingvcn"></a>**StartingVcn**  
FSCTL\_GET\_取得\_ポインターが、エクステントと、関連付けられた仮想および論理クラスター番号の列挙を開始するときに使用する VCN。 \_FSCTL のファイルシステム制御コードを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を初めて呼び出すときに、\_ポインター\_取得するには、 **StartingVcn**を0に設定する必要があります。

*Outputbuffer*がファイルの vcns とエクステントのマップ全体を格納するのに十分な大きさではない場合、呼び出し元は、取得\_\_ポインターの**nextvcn**メンバーで返される値を使用して、より多くのマップデータを要求する必要があります。VCN を開始しています。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
InputBuffer の入力バッファーの長さ (バイト単位) *。*

<a href="" id="outputbuffer"></a>*OutputBuffer*  
代替ストリーム、ファイル、またはディレクトリに対応するディスク上のエクステントの列挙体を含む、型取得\_ポインター\_ポインターの可変サイズ構造体へのポインター。

```cpp
typedef struct RETRIEVAL_POINTERS_BUFFER {
 ULONG  ExtentCount;
  LARGE_INTEGER  StartingVcn;
 struct {
    LARGE_INTEGER  NextVcn;
    LARGE_INTEGER  Lcn;
  } Extents[1];
} RETRIEVAL_POINTERS_BUFFER, *PRETRIEVAL_POINTERS_BUFFER;
```

**属する**

<a href="" id="extentcount"></a>**ExtentCount**  
**エクステント**配列内の要素の数。

<a href="" id="startingvcn"></a>**StartingVcn**  
関数呼び出しによって返された VCN を開始しています。 これは必ずしも関数呼び出しによって要求される VCN とは限りません。ファイルシステムドライバーは、要求された開始 VCN が検出されたエクステントの最初の VCN に切り捨てられる可能性があるためです。

<a href="" id="extents-"></a>**エクステント**   
エクステント構造体の配列。 配列内のメンバーの数については、「 **ExtentCount**」を参照してください。 配列の各メンバーには、次のメンバーがあります。

<a href="" id="nextvcn"></a>**NextVcn**  
次のエクステントが開始される VCN。 この値は、 **StartingVcn** (最初の**エクステント**配列メンバーの場合) または配列の前のメンバーの**nextvcn** (他のすべての**エクステント**配列メンバーの場合) のいずれかを差し引いた値で、現在のエクステントのクラスター単位の長さになります。

<a href="" id="lcn"></a>**Lcn**  
ボリュームで現在のエクステントが開始される LCN。 NTFS では、値 (LONGLONG)-1 は、部分的に割り当てられた圧縮ユニット、またはスパースファイルの未割り当て領域のいずれかを示します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。

<a name="status-block"></a>状態ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)と[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)はどちらも STATUS\_SUCCESS または適切な NTSTATUS エラー値を返します。

VCN/extents マップが*Outputbuffer*に収まらない場合、どちらのルーチンも STATUS\_BUFFER\_OVERFLOW という値を返し、呼び出し元は取得の**nextvcn**メンバーで返された値を使用して、より多くのマップデータを要求する必要があり\_ポインターは、 [**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)への次の呼び出しで、バッファー構造を開始 VCN (**StartingVcn**) として\_します。

**StartingVcn**で指定された値がファイルの末尾を越えている場合は、\_ファイルの\_end\_が返されます。

<a name="remarks"></a>解説
-------

FastFAT と exFAT デバイスでは、 **FSCTL\_GET\_取得\_ポインター**制御コードを使用できます。 この機能は、フラッシュドライブなどのデバイスでの BitLocker の使用をサポートしています。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






