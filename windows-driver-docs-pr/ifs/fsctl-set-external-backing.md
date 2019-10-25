---
title: FSCTL_SET_EXTERNAL_BACKING 制御コード
description: '\_外部制御コード\_設定された FSCTL\_は、外部バッキングプロバイダーによって、Windows イメージフォーマット (WIM) ファイルや圧縮ファイルなどのファイルのバッキングソースを設定します。'
ms.assetid: 5CB9FD4D-AF29-4438-B0B5-49871102968A
keywords:
- FSCTL_SET_EXTERNAL_BACKING 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703bc6cada1475c12ee16965770d381b24f51c5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841253"
---
# <a name="fsctl_set_external_backing-control-code"></a>FSCTL\_設定\_外部\_バッキングコントロールコード


**\_外部制御コード\_設定**された FSCTL\_は、外部バッキングプロバイダーによって、Windows イメージフォーマット (WIM) ファイルや圧縮ファイルなどのファイルのバッキングソースを設定します。 外部でサポートされるファイルのコンテンツは、ファイルが存在するボリューム以外のボリュームで発生する可能性があります。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 バッキングが設定されているファイルのファイルポインターオブジェクト。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 バッキングが設定されているファイルのハンドル。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作を行うには、FSCTL\_使用して **\_外部\_を設定**します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
入力バッファーへのポインター。これには、 [**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体の後にプロバイダーデータが格納されます。 WIM によってサポートされるファイルの場合、 **WOF\_外部\_情報**の後に[**wim\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)構造が続きます。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
*InputBuffer*で提供されるデータのサイズ。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
なし。 を NULL に設定します。

<a href="" id="outputbufferlength--in-"></a> *\]の OutputBufferLength \[*  
を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合は、適切な NTSTATUS 値が返されます。

<a name="remarks"></a>注釈
-------

追加されたデータソースのバッキングプロバイダーが WIM プロバイダーである場合、入力バッファーには、[**外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造に加えて、 [**wim\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)構造が\_含まれます。 この場合、 *Inputbufferlength*は**sizeof**(**WOF\_外部\_info**) + **sizeof**(**WIM\_PROVIDER\_外部\_INFO**) になります。

個別に圧縮されたファイルは、変更されないデータ (実行可能ファイルを含む) に適した圧縮を提供します。 これらが書き込み用に開かれている場合、ファイルは透過的に圧縮解除されます。 個別に圧縮されたファイルを指定するために、入力バッファーには、外部[ **\_情報\_V1 構造\_ファイル\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_provider_external_info_v1) 、 [ **\_の\_外部の情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造が含まれます。 この場合、 *Inputbufferlength*は**sizeof**(**WOF\_外部\_info**) + **sizeof**(**ファイル\_プロバイダー\_外部\_情報\_V1**) になります。 個々の圧縮ファイルは、Windows 10 以降で使用できます。

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

[**FSCTL\_\_外部\_の削除**](fsctl-delete-external-backing.md)

[**FSCTL\_外部\_バッキング\_取得する**](fsctl-get-external-backing.md)

[**WIM\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_external_info)

[**WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

 






