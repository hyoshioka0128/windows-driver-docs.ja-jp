---
title: FSCTL_ENUM_OVERLAY 制御コード
description: FSCTL\_ENUM\_オーバーレイコントロールコードは、指定されたボリュームのバッキングプロバイダーからすべてのデータソースを列挙します。
ms.assetid: 146A7D77-034F-4C06-99B8-8EBA6E7F0A40
keywords:
- FSCTL_ENUM_OVERLAY 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_ENUM_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc2652b99b14e4eb494a9bc5c461e6dbe4fcd8c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841314"
---
# <a name="fsctl_enum_overlay-control-code"></a>FSCTL\_ENUM\_オーバーレイコントロールコード


**FSCTL\_ENUM\_オーバーレイ**コントロールコードは、指定されたボリュームのバッキングプロバイダーからすべてのデータソースを列挙します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 マウントを解除するボリュームを指定するファイルポインターオブジェクト。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 マウントを解除するボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作には、FSCTL\_使用して **\_オーバーレイを削除**してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
入力バッファーへのポインター。これには、 [**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体が含まれている必要があります。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
**Sizeof**(WOF\_外部\_INFO) に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
ボリュームをバックアップするデータソースの[ **\_オーバーレイ\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input)構造を1つ以上持つ WIM\_プロバイダーを受け取る出力バッファーへのポインター。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*Outputbuffer*によってポイントされるバッファーのサイズ (バイト単位)。

<a href="" id="lengthreturned--out-"></a>*長さが \[out を返しました\]*  
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
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>要求元には管理者特権がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>Outputbuffer</em>によってポイントされ、 <em>outputbufferlength</em>によって指定された出力バッファーの長さが小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>要求されたボリュームにアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バッキングサービスが存在しないか、開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

WIM プロバイダーのデータソースを列挙すると、出力バッファーに[**wim\_プロバイダーの配列\_オーバーレイ\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input)構造が格納されます。 出力バッファーのサイズは、すべてのオーバーレイエントリを格納するのに十分な大きさである必要があります。または、呼び出しによってステータス\_バッファー\_\_小さすぎます。

追加のバッキングプロバイダーは、独自の特定の列挙構造を定義します。

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

[**FSCTL\_\_オーバーレイの追加**](fsctl-add-overlay.md)

[**WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

 






