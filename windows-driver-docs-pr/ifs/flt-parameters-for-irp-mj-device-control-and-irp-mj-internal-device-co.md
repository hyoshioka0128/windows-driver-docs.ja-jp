---
title: FLT_PARAMETERS IRP_MJ_DEVICE_CONTROL と IRP_MJ_INTERNAL_DEVICE_CONTROL 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_デバイス\_コントロールまたは IRP\_MJ\_内部\_デバイス\_コントロール。
ms.assetid: ed2da1d5-838e-41a4-9a26-c61518da9cf3
keywords:
- FLT_PARAMETERS IRP_MJ_DEVICE_CONTROL と IRP_MJ_INTERNAL_DEVICE_CONTROL 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: b6fd864392861c19ed7060d4afdf63b31a008360
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386081"
---
# <a name="fltparameters-for-irpmjdevicecontrol-and-irpmjinternaldevicecontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_デバイス\_コントロールと IRP\_MJ\_内部\_デバイス\_コントロール共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
    } Common;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Neither;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   SystemBuffer;
    } Buffered;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputSystemBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Direct;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputBuffer;
      PVOID                   OutputBuffer;
    } FastIo;
  } DeviceIoControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**DeviceIoControl**  
**一般的です**  
バッファリングのすべてのメソッドで使用されるコンポーネントの共用体。

**OutputBufferLength**  
バッファーのバイト単位の長さを**Neither.OutputBuffer**、 **Direct.OutputBuffer**、または**FastIo.OutputBuffer**へのポインターします。

**InputBufferLength**  
バッファーのバイト単位の長さを**Neither.InputBuffer**、 **Buffered.SystemBuffer**、 **Direct.InputSystemBuffer**、または**FastIo.InputBuffer**へのポインターします。

**IoControlCode**  
ターゲット デバイスのデバイス ドライバーに渡される IOCTL 関数コードです。

IOCTL 要求の詳細については、次を参照してください[I/O 制御コードを使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*と"デバイスの入力と出力の制御コード"、Microsoft Windows sdk。ドキュメントです。 (このリソースできない場合がありますのいくつかの言語および国。)

**どちらも**  
共用体のコンポーネントがバッファー メソッドがメソッドである場合に使用\_NEITHER します。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*します。

**InputBuffer**  
操作の元の要求者が提供される入力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)、 [ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)と[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)と[ユーザー スペースのアドレスを参照するエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)、 [ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)と[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)と[ユーザー スペースのアドレスを参照するエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)で、*カーネル モードのアーキテクチャ ガイド*します。

**OutputMdlAddress**  
バッファーを記述したメモリ記述子一覧 (MDL) のアドレスを*Neither.OutputBuffer*へのポインターします。 このメンバーは省略可能とは、 **NULL**します。

**バッファー**  
共用体のコンポーネントがバッファー メソッドがメソッドである場合に使用\_バッファーに格納されました。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**SystemBuffer**  
操作のシステムによって割り当てられたバッファーのアドレス。 メソッドで\_バッファー I/O、このバッファーが使用されるの入力し、出力の両方。 詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**ダイレクト**  
共用体のコンポーネントがバッファー メソッドがメソッドである場合に使用\_IN\_ダイレクトまたはメソッド\_アウト\_ダイレクトします。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**InputSystemBuffer**  
操作の入力バッファーのアドレス。 このバッファーに安全にカーネル モードからアクセスできるように、オペレーティング システムによってダウン ロックされています。 詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 メソッドとは異なり、直接 i/o\_I/O のどちらも、オペレーティング システムがロック ダウンこのバッファーはカーネル モードからにアクセスする安全なミニフィルターが I/O 操作の元の要求者と同じプロセス コンテキストである限りようにします。 (それ以外の場合に呼び出す必要があります[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)にメモリの記述子のリスト (MDL) からシステムのアドレスを取得、 **OutputMdlAddress**へのポインター.)詳細については、次を参照してください。[を使用して直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o)と[ダイレクト I/O エラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputMdlAddress**  
MDL バッファーを記述するアドレスを**Direct.OutputBuffer**へのポインターします。 このメンバーが必要とすることはできません**NULL**します。

**FastIo**  
共用体のコンポーネントで使用されるときに、 [ **FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)構造が高速な I/O IRP を表す\_MJ\_デバイス\_コントロール操作です。

**InputBuffer**  
操作の元の要求者が提供される入力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)、 [ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)と[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[ユーザー スペースのアドレスを参照するエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)、 [ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)と[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[ユーザー スペースのアドレスを参照するエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)の構造体[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)操作には、IRP ベースのパラメーターが含まれています。コールバック データによって表されるデバイス-I/O-制御情報操作 ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体。

IRP\_MJ\_デバイス\_IRP ベース操作または I/O 操作が高速コントロールであることができます。

IRP\_MJ\_内部\_デバイス\_コントロールは IRP ベースの I/O 操作です。

<a name="requirements"></a>必要条件
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

[**FltDeviceIoControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IRP\_MJ\_DEVICE\_CONTROL**](irp-mj-device-control.md)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






