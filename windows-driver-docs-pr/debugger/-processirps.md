---
title: processirps
description: Processirps 拡張機能では、プロセスに関連付けられている I/O 要求パケット (Irp) に関する情報が表示されます。
ms.assetid: B7CC72A5-7D3F-4DE5-878D-ABD08BAF227C
keywords:
- Windows デバッグ processirps
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- processirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0cb71473f05a9b37314bf709b23bade760e63a6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334344"
---
# <a name="processirps"></a>!processirps


**! Processirps**拡張機能は、プロセスに関連付けられている I/O 要求パケット (Irp) に関する情報を表示します。

```dbgcmd
!processirps
!processirps ProcessAddress [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_ProcessAddress"></span><span id="_processaddress"></span><span id="_PROCESSADDRESS"></span> **** *ProcessAddress*  
プロセスのアドレス。 指定した場合*ProcessAddress*だけ Irp に関連付けられているプロセスが表示されます。 指定しない場合*ProcessAddress*、すべてのプロセスの Irp が表示されます。

<span id="_Flags"></span><span id="_flags"></span><span id="_FLAGS"></span> **** *フラグ*  
次のフラグの 1 つ以上のビットごとの OR。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示の Irp では、スレッドにキューに置かれました。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示の Irp では、ファイル オブジェクトをキューに置かれました。

指定した場合*フラグ*、指定する必要がありますも*ProcessAddress*します。 指定しない場合*フラグ*Irp が両方のスレッドにキューに配置され、ファイル オブジェクトが表示されます。

## <span id="ddk__processfields_dbg"></span><span id="DDK__PROCESSFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

kdexts.dll

<a name="remarks"></a>注釈
-------

このコマンドでは、プロセスのキューに置かれた Irp のスレッドのキューに格納されているとは、ファイル オブジェクトをキューに登録される両方をすばやく特定することができます。 Irp では、ファイル オブジェクトに関連付けられている完了ポートがあるときに、ファイル オブジェクトをキューに登録します。

<a name="examples"></a>例
--------

使用することができます[ **! プロセス**](-process.md)プロセスのアドレスを取得するコマンド。 たとえば、explorer.exe のプロセスのアドレスを取得できます。

```dbgcmd
2: kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
...
PROCESS fffffa800688c940
    SessionId: 1  Cid: 0bbc    Peb: 7f70da5e000  ParentCid: 0b84
    DirBase: 2db10000  ObjectTable: fffff8a0025bd440  HandleCount: 1056.
    Image: explorer.exe
```

Explorer.exe プロセスのアドレスを渡すことができますので、 **! processirps**コマンド。 次の出力では、その explorer.exe がスレッドに Irp がキューに登録され、ファイル オブジェクトに Irp がキューに登録します。

```dbgcmd
2: kd> !processirps fffffa800688c940
**** PROCESS fffffa800688c940 (Image: explorer.exe) ****

Checking threads for IRPs.

  Thread fffffa800689f080:

    IRP fffffa80045ccc10 - Owned by \FileSystem\Ntfs for device fffffa8004f5c030
    IRP fffffa800454f650 - Owned by \FileSystem\Ntfs for device fffffa8004f5c030
    ...
    IRP fffffa80068e9c10 - Owned by \FileSystem\Ntfs for device fffffa8004f5c030

Checking file objects for IRPs.

  FileObject fffffa80068795e0 (handle 8bc):

    IRP fffffa8006590cf0 - Owned by \Driver\DeviceApi for device DeviceApi (fffffa800363ae40)

  ...

  FileObject fffffa8005bf59c0 (handle 900):

    IRP fffffa8006659010 - Owned by \Driver\DeviceApi for device DeviceApi (fffffa800363ae40)
```

 

 





