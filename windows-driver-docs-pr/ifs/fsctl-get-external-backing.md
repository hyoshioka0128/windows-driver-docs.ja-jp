---
title: FSCTL_GET_EXTERNAL_BACKING 制御コード
description: FSCTL\_GET\_外部\_バッキングコントロールコードは、外部のバッキングプロバイダーからファイルのバッキング情報を取得します。
ms.assetid: 18A8E71E-CAED-4E0A-95D0-18E99F9733B2
keywords:
- FSCTL_GET_EXTERNAL_BACKING 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_GET_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6861118c45047353eab364118fccfc3f7f9effe0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841308"
---
# <a name="fsctl_get_external_backing-control-code"></a>FSCTL\_外部\_バッキングコントロールコード\_取得する


**FSCTL\_GET\_外部\_バッキング**コントロールコードは、外部のバッキングプロバイダーからファイルのバッキング情報を取得します。 バッキングプロバイダーには、Windows イメージフォーマット (WIM) プロバイダーまたは個々の圧縮ファイルプロバイダーが含まれます。 外部でサポートされるファイルのコンテンツは、照会されたファイルを含むボリューム以外のボリューム上に存在する可能性があります。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 バッキング情報を照会する対象のファイルのファイルポインターオブジェクト。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 バッキング情報のクエリ対象となるファイルのハンドル。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作を行うには、FSCTL\_使用して**外部\_\_取得**します。

<a href="" id="inputbuffer--in-"></a> *\]の InputBuffer \[*  
なし。 を**NULL**に設定します。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
を0に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
出力バッファーへのポインター。これには、 [**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体の後にプロバイダーデータが格納されるのに十分なサイズが必要です。 WIM によってサポートされるファイルの場合、 **WOF\_外部\_情報**の後に[**wim\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)構造が続きます。 個別に圧縮されたファイルの場合、 **WOF\_外部\_情報**の後に[**ファイル\_プロバイダー\_外部\_情報\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_provider_external_info_v1)構造が続きます。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*Outputbuffer*が指すバッファーのサイズ (バイト単位)。

<a href="" id="lengthreturned"></a>*返される長さ*  
正常に完了したときに*Outputbuffer*に書き込まれるバイト数を指定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、次のいずれかの NTSTATUS 値を返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_OBJECT_NOT_EXTERNALLY_BACKED</strong></p></td>
<td align="left"><p>ファイルが外部でサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バッキングサービスが存在しないか、開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

更新するデータソースのバッキングプロバイダーが WIM ファイルの場合、出力バッファーには、外部[ **\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体の後に[**wim\_プロバイダー\_外部\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)構造体が\_含まれます。 *Outputbufferlength*は、少なくとも**sizeof**(WOF\_外部\_info) + **sizeof**(WIM\_PROVIDER\_外部\_info) である必要があります。 バッキングプロバイダーが個別に圧縮されたファイルの場合、出力バッファーには、外部[ **\_情報\_V1 構造を\_ファイル\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_provider_external_info_v1)の **\_\_外部の情報**構造が格納されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1 更新プログラムから使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**外部\_バッキング\_FSCTL\_設定**](fsctl-set-external-backing.md)

[**WIM\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)

[**WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

 






