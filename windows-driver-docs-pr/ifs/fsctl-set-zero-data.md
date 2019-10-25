---
title: FSCTL_SET_ZERO_DATA 制御コード
description: FSCTL\_\_ゼロ (0) のファイルの指定された範囲を fill\_データコントロールコードに設定します。
ms.assetid: AEC4DAD4-17EB-412B-881B-E54F6A578637
keywords:
- FSCTL_SET_ZERO_DATA 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_ZERO_DATA
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2b723eeb510e387efb42a8e154cf49b0d483340
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841247"
---
# <a name="fsctl_set_zero_data-control-code"></a>FSCTL\_\_ゼロ\_データ制御コードに設定


**FSCTL\_\_ゼロ**(0) のファイルの指定された範囲を FILL\_データコントロールコードに設定します。 ファイルがスパースまたは圧縮されている場合は、NTFS ファイルシステムによってファイル内のディスク領域の割り当てが解除されることがあります。 これにより、ファイルサイズを拡張せずに、バイトの範囲がゼロ (0) に設定されます。

ドライバーからこの操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)を呼び出します。

**Parameters**

<a href="" id="instance"></a>*Instance*  
呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fileobject"></a>*ファ*  
0を書き込むファイルへのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。

この操作では、FSCTL\_使用して **\_ゼロ\_データを設定**します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
ファイルへのポインターは、0に設定するファイルの範囲を指定するデータ\_情報または[**ファイル\_\_ゼロ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex) [ **\_データ情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information)またはファイルを\_ます。

**Fileoffset**メンバーは、ゼロ (0) に設定する最初のバイトのバイトオフセットです。また、 **BeyondFinalZero**メンバーは、最後のゼロ (0) バイトを超える最初のバイトのバイトオフセットです。

ファイルの**Flags**メンバー [ **\_0\_データ\_情報\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex)は操作の修飾子を指定します。 たとえば、**フラグ**が**file\_0\_data\_INFORMATION\_フラグ**に設定され\_キャッシュされた\_データ\_保持する場合、ファイルのこの範囲に対応するキャッシュの内容は削除されません。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
入力バッファーのサイズ (バイト単位)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。を**NULL**に設定します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)は、 **STATUS\_SUCCESS**または適切な NTSTATUS 値を返します。

-   操作を完了するために必要なメモリが不足している場合は、**状態 \_\_リソース**が返されます。
-   **ステータス\_無効\_パラメーター**が返されるのは、 *Inputbufferlength*がファイルのサイズよりも小さい場合 **\_0\_データ\_情報**構造体、または指定されたファイルがシステムメタデータファイルである場合です。またはディレクトリ。
-   **ファイル\_0\_データ\_情報\_フラグ**\_\_キャッシュされている\_データがユーザーモードから設定されている場合、 **\_アクセス\_拒否**された状態が返されます。
-   ボリュームが現在書き込み保護されている場合、**状態\_メディア\_書き込み\_保護**されます。

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
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ファイル\_ゼロ\_データ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information)

[**ファイル\_ゼロ\_データ\_情報\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_zero_data_information_ex)

 

 






