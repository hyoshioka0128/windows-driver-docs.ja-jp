---
title: FLT_PARAMETERS for IRP_MJ_DEVICE_CONTROL and IRP_MJ_INTERNAL_DEVICE_CONTROL union
description: FLT\_IO\_パラメーターの MajorFunction フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネントは、IRP\_MJ\_デバイス\_CONTROL または IRP\_MJ\_内部\_デバイス\_コントロール。
ms.assetid: ed2da1d5-838e-41a4-9a26-c61518da9cf3
keywords:
- FLT_PARAMETERS for IRP_MJ_DEVICE_CONTROL and IRP_MJ_INTERNAL_DEVICE_CONTROL union インストール可能なファイルシステムドライバー
- FLT_PARAMETERS union にインストール可能なファイルシステムドライバー
- PFLT_PARAMETERS union ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: a217db598899e9206e3bcf405d79c39aed7cd538
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841387"
---
# <a name="flt_parameters-for-irp_mj_device_control-and-irp_mj_internal_device_control-union"></a>\_IRP\_MJ\_デバイス\_コントロールおよび IRP\_MJ\_内部\_デバイス\_コントロール共用体


[**FLT\_IO\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)の**MajorFunction**フィールド\_操作のブロック構造体が[**irp\_MJ\_デバイス\_CONTROL**](irp-mj-device-control.md)または[**irp\_MJ の場合に使用される共用体コンポーネント\_内部\_デバイス\_制御**](irp-mj-internal-device-control.md)。

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

<a name="members"></a>Members
-------

**DeviceIoControl**  
**的**  
すべてのバッファリングメソッドに使用される共用体コンポーネント。

**OutputBufferLength**  
出力バッファーの長さ (バイト単位 **)。 outputbuffer、** **Direct**Buffer、または**fadirectory**のメンバーはを指します。

**InputBufferLength**  
**InputBuffer**、**バッファーに格納**さ**れ**ていない、InputBuffer、または**fa**のメンバーが指すバッファーの長さ (バイト単位)。

**IoControlCode**  
ターゲットデバイスのデバイスドライバーに渡される IOCTL 関数コード。

IOCTL 要求の詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」および Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**両者**  
バッファリングメソッドがメソッド\_場合に使用される共用体コンポーネントではありません。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。

**InputBuffer**  
操作の元の要求元が指定した入力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[バッファーを使用し](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)た[ユーザー領域のアドレスの参照](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**  
操作の元の要求元が指定した出力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[バッファーを使用し](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)た[ユーザー領域のアドレスの参照](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)」を参照してください。

**OutputMdlAddress**  
*Outputbuffer*メンバーが指しているバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

**付き**  
バッファリングメソッドがメソッド\_バッファリングされるときに使用される共用体コンポーネント。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**SystemBuffer**  
操作に対してシステムが割り当てたバッファーのアドレス。 メソッド\_バッファー i/o では、このバッファーは入力と出力の両方に使用されます。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**接続**  
バッファリングメソッドが\_ダイレクトまたはメソッドで\_メソッドである場合に使用される共用体コンポーネントは\_ダイレクト\_OUT ます。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**InputSystemBuffer**  
操作の入力バッファーのアドレス。 このバッファーは、カーネルモードから安全にアクセスできるように、オペレーティングシステムによってロックされています。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**  
操作の元の要求元が指定した出力バッファーのユーザーモード仮想アドレス。 ダイレクト i/o では、i/o 操作の元の要求元と同じプロセスコンテキストでミニフィルターが使用されている限り、オペレーティングシステムは i/o ではない\_方法で、このバッファーをロックダウンして、カーネルモードから安全にアクセスできるようにします。 (それ以外の場合は、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出して、 **Outputmdladdress**メンバーが指すメモリ記述子リスト (MDL) からシステムアドレスを取得する必要があります)。詳細については、「*カーネルモードアーキテクチャガイド*」の「direct I/o と[エラーをダイレクト I/o で](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)[使用する](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputMdlAddress**  
**直接の outputbuffer**メンバーが指すバッファーを記述する MDL のアドレス。 このメンバーは必須であり、 **NULL**にすることはできません。

**高速**  
[**FLT\_CALLBACK\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)構造体が高速 i/o IRP\_MJ\_デバイス\_制御操作を表す場合に使用される共用体コンポーネント。

**InputBuffer**  
操作の元の要求元が指定した入力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[ユーザー空間の参照」のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**  
操作の元の要求元が指定した出力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[ユーザー空間の参照」のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)を参照してください。 (このリソースは、一部の言語および国では使用できません。)

<a name="remarks"></a>注釈
-------

[**Irp\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)と[**irp\_MJ\_内部\_デバイス**](irp-mj-internal-device-control.md)の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、irp ベースのパラメーターが含まれています。コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造によって表されるデバイス-i/o 制御情報操作。 これは、 [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

IRP\_MJ\_デバイス\_制御は、IRP ベースの操作または高速 i/o 操作にすることができます。

IRP\_MJ\_内部\_デバイス\_制御は、IRP ベースの i/o 操作です。

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
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltDeviceIoControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






