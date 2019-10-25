---
title: FSCTL_DISMOUNT_VOLUME 制御コード
description: ボリュームが使用されているかどうかに関係なくボリュームのマウントを解除しようとすると、FSCTL\_\_ボリューム制御コードがマウント解除されます。
ms.assetid: edfff768-3bb3-4b8a-b982-80797ac116fd
keywords:
- FSCTL_DISMOUNT_VOLUME 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_DISMOUNT_VOLUME
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7592bdc7d22a93abfb630d2ed6b2360399914c09
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841321"
---
# <a name="fsctl_dismount_volume-control-code"></a>FSCTL\_マウント解除\_ボリューム制御コード


ボリュームが使用されているかどうかに関係なくボリュームのマウントを解除しようとすると、 **FSCTL\_\_ボリューム**制御コードがマウント解除されます。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**パラメーター**

<a href="" id="instance"></a>*Instance*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 マウントを解除するボリュームを指定するファイルポインターオブジェクト。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 マウントを解除するボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作には、FSCTL\_使用して **\_ボリュームのマウントを解除**してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。 を**NULL**に設定します。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
この操作では使用されません。 を0に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
この操作では使用されません。 を**NULL**に設定します。

<a href="" id="outputbufferlength--in-"></a> *\]の OutputBufferLength \[*  
この操作では使用されません。 を0に設定します。

<a name="status-block"></a>状態ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、STATUS\_SUCCESS または適切な NTSTATUS 値を返します。

<a name="remarks"></a>解説
-------

ボリューム制御コード **\_\_マウント解除**すると、他のプロセスがボリュームを使用しているかどうかに関係なく、ボリュームのマウントを解除しようとします。ボリュームのロックを保持していない場合、これらのプロセスに対して予期しない結果が生じる可能性があります。 ボリュームのロックの詳細については、「 [**FSCTL\_LOCK\_volume**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_lock_volume)」を参照してください。

オペレーティングシステムは、マウント解除されたボリュームを検出しません。 マウント解除されたボリュームにアクセスしようとすると、オペレーティングシステムはボリュームのマウントを試みます。 たとえば、 [**Getlogicaldrives**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getlogicaldrives)を呼び出すと、マウント解除されたボリュームをマウントするオペレーティングシステムがトリガーされます。

[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)に渡される*FileHandle*ハンドルは、直接アクセスするために開かれたボリュームへのハンドルである必要があります。 ボリュームハンドルを取得するには、 *Objectattributes*パラメーターを\\\\の形式の*ObjectName*に設定して[**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)を呼び出します *。\\x:* ここで、 *x*はボリュームのドライブ文字、フロッピーディスクです。ドライブ、または CD-ROM ドライブ。 また、アプリケーションでは、 **Zwcreatefile**の共有*アクセス*パラメーターで書き込みフラグ\_\_共有\_ファイルを共有\_指定する必要があります。

指定されたボリュームがシステムボリュームであるか、またはページファイルを含んでいる場合、操作は失敗します。

指定されたボリュームが別のプロセスによってロックされている場合、操作は失敗します。

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
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






