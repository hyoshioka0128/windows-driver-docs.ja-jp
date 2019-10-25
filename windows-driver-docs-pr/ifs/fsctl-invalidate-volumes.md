---
title: FSCTL_INVALIDATE_VOLUMES 制御コード
description: FSCTL\_は、指定されたファイルオブジェクトまたはハンドルによって表されるデバイス上にマウントされているすべてのボリュームを検出して削除\_ボリューム制御コードが検出し、削除します。
ms.assetid: 26B7EBA2-F3A9-4E5A-961C-C1857AA4FF33
keywords:
- FSCTL_INVALIDATE_VOLUMES 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_INVALIDATE_VOLUMES
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df174ddb9ebd9b9e81f0be46285b10d4aab1c0ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841299"
---
# <a name="fsctl_invalidate_volumes-control-code"></a>FSCTL\_\_ボリューム制御コードの無効化


FSCTL\_は、指定されたファイルオブジェクトまたはハンドルによって表されるデバイス上にマウントされているすべてのボリュームを検出して削除 **\_ボリューム**制御コードが検出し、削除します。

この操作を実行するには、ミニフィルタードライバーが[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)を呼び出します。また、ファイルシステム、リダイレクター、およびレガシファイルシステムフィルタードライバーは、次のパラメーターを使用して[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**パラメーター**

<a href="" id="fileobject"></a>*ファ*  
デバイスへのハンドル。 デバイスハンドルを取得するには、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数を呼び出します。

<a href="" id="filehandle"></a>*FileHandle*  
デバイスへのハンドル。 デバイスハンドルを取得するには、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数を呼び出します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作では、FSCTL\_使用して **\_ボリュームを無効**にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。を**NULL**に設定します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。を0に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。を**NULL**に設定します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>状態ブロック
------------

操作が成功した場合、または適切な NTSTATUS 値が返された場合、 [**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)と[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462) STATUS\_SUCCESS を返します。

<a name="remarks"></a>解説
-------

FSCTL\_は、ボリュームデバイスオブジェクトではなく、ファイルシステムのコントロール (名前付き) デバイスオブジェクトに\_ボリュームが送信されます。 コントロールデバイスオブジェクトの詳細については、「[コントロールデバイスオブジェクトの作成](https://docs.microsoft.com/windows-hardware/drivers/ifs/creating-the-control-device-object)」を参照してください。

FAT および NTFS ファイルシステムは、IRP\_MJ\_PNP/\_IRP に応答することによって、突然の削除を処理します。これにより、突然\_削除が\_されます。

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

 

 






