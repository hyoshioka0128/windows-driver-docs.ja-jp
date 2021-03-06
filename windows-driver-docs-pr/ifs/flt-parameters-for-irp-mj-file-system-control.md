---
title: FLT_PARAMETERS IRP_MJ_FILE_SYSTEM_CONTROL 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_ファイル\_システム\_コントロール。
ms.assetid: d90b9f23-9fae-46e8-b68c-1ba11b3fa17a
keywords:
- FLT_PARAMETERS IRP_MJ_FILE_SYSTEM_CONTROL 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 3cc5a94d870d3ae5e12891bcc8689c0166035bbb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380350"
---
# <a name="fltparameters-for-irpmjfilesystemcontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_ファイル\_システム\_コントロール共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が[ **IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      PVPB           Vpb;
      PDEVICE_OBJECT DeviceObject;
    } VerifyVolume;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
    } Common;
    struct {
      ULONG                    OutputBufferLength;
      ULONG POINTER_ALIGNMENT  InputBufferLength;
      ULONG POINTER_ALIGNMENT  FsControlCode;
      PVOID                    InputBuffer;
      PVOID                    OutputBuffer;
      PMDL                     OutputMdlAddress;
    } Neither;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
      PVOID                   SystemBuffer;
    } Buffered;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
      PVOID                   InputSystemBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Direct;
  } FileSystemControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**FileSystemControl**  
次のメンバーを含む構造体。

**VerifyVolume**  
IRP に使用される共用体のコンポーネント\_MN\_確認\_ボリューム操作。

**Vpb**  
検証するボリュームのボリューム パラメーター ブロック (VPB) へのポインター。

**デバイス オブジェクト**  
検証するボリュームのデバイス オブジェクトへのポインター。

**一般的です**  
IRP のすべてのバッファリング メソッドに使用される共用体のコンポーネント\_MN\_カーネル\_呼び出しと IRP\_MN\_ユーザー\_FS\_要求の操作。

**OutputBufferLength**  
バッファーのバイト単位の長さを**Neither.OutputBuffer**または**Direct.OutputBuffer**へのポインターします。

**InputBufferLength**  
バッファーのバイト単位の長さを**Neither.InputBuffer**、 **Buffered.SystemBuffer**、または**Direct.InputSystemBuffer**へのポインターします。

**FsControlCode**  
ターゲット デバイスのファイル システム、ファイル システム フィルターまたはミニフィルター ドライバーに渡される FSCTL 関数コードです。

IOCTL および FSCTL 要求の詳細については、次を参照してください[I/O 制御コードを使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*と"デバイスの入力と出力の制御コード"、Microsoft Windows sdk。ドキュメントです。 (このリソースできない場合がありますのいくつかの言語および国。)

**どちらも**  
IRP に使用される共用体のコンポーネント\_MN\_カーネル\_呼び出しと IRP\_MN\_ユーザー\_FS\_要求操作は、バッファリングのメソッドは、メソッドと\_NEITHER. バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**InputBuffer**  
操作の元の要求者が提供される入力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)、 [ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)と[ **MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)と[ユーザー スペースのアドレスを参照するエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)、 [ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)と[ **MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)と[ユーザー スペースのアドレスを参照するエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputMdlAddress**  
バッファーを記述したメモリ記述子一覧 (MDL) のアドレスを**Neither.OutputBuffer**へのポインターします。 このメンバーは省略可能とは、 **NULL**します。

**バッファー**  
IRP に使用される共用体のコンポーネント\_MN\_カーネル\_呼び出しと IRP\_MN\_ユーザー\_FS\_要求操作は、バッファリングのメソッドは、メソッドと\_バッファーに格納します。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**SystemBuffer**  
操作のシステムによって割り当てられたバッファーのアドレス。 メソッドで\_バッファー I/O、このバッファーが使用されるの入力し、出力の両方。 詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**ダイレクト**  
IRP に使用される共用体のコンポーネント\_MN\_カーネル\_呼び出しと IRP\_MN\_ユーザー\_FS\_要求操作は、バッファリングのメソッドは、メソッドと\_で\_ダイレクト メソッド、または\_アウト\_ダイレクトします。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*します。

**InputSystemBuffer**  
操作の入力バッファーのアドレス。 このバッファーに安全にカーネル モードからアクセスできるように、オペレーティング システムによってダウン ロックされています。 詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 メソッドとは異なり、直接 i/o\_I/O のどちらも、オペレーティング システムがロック ダウンこのバッファーはカーネル モードからにアクセスする安全なミニフィルターが I/O 操作の元の要求者と同じプロセス コンテキストである限りようにします。 (それ以外の場合に呼び出す必要があります[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)に MDL からシステムのアドレスを取得、 **OutputMdlAddress**へのポインターします)。詳細については、次を参照してください。[を使用して直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o)と[ダイレクト I/O エラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputMdlAddress**  
MDL バッファーを記述するアドレスを**Direct.OutputBuffer**へのポインターします。 このメンバーが必要とすることはできません**NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)の構造体[ **IRP\_MJ\_ファイル\_システム\_コントロール** ](irp-mj-file-system-control.md)操作にはコールバック データによって表されるファイル システムの制御情報操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体。

IRP\_MJ\_ファイル\_システム\_コントロールが IRP ベースの操作。

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


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoVerifyVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ioverifyvolume)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






