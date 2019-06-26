---
title: wdfkd.wdflogdump
description: Wdfkd.wdflogdump 拡張機能では、KMDF ドライバーまたは UMDF 2 ドライバーの使用可能な場合、WDF インフライト レコーダーのログ レコードが表示されます。
ms.assetid: da03fafe-4cc8-4da6-9795-828e69e0df20
keywords:
- デバッグ wdfkd.wdflogdump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdflogdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbd8b3f6ac3bb3f83cc697bc8fb902a863670161
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362406"
---
# <a name="wdfkdwdflogdump"></a>!wdfkd.wdflogdump


**! Wdfkd.wdflogdump**拡張機能では、KMDF ドライバーまたは UMDF 2 ドライバー可能であれば、WDF インフライト レコーダーのログ レコードが表示されます。 このコマンドを使用することができます、[完全メモリ ダンプ](complete-memory-dump.md)、[カーネル メモリ ダンプ](kernel-memory-dump.md)、または[ライブのカーネル モード ターゲット](live-kernel-mode-targets.md)。

KMDF

```dbgcmd
!wdfkd.wdflogdump [DriverName][WdfDriverGlobals][-d | -f | -a LogAddress]
```

UMDF

```dbgcmd
!wdfkd.wdflogdump  [DriverName.dll][HostProcessId][-d | -f | -m]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
-   KMDF:KMDF ドライバーの名前。 名前は、.sys ファイル名の拡張子を含めることはできません。
-   UMDF:2 の UMDF ドライバーの名前。 名前は、.dll ファイル名の拡張子を含める必要があります。

<span id="_______Parameter2______"></span><span id="_______parameter2______"></span><span id="_______PARAMETER2______"></span> *パラメーター 2*   
-   KMDF:*WdfDriverGlobals* -のアドレス、 *WdfDriverGlobals*構造体。 実行して、このアドレスを決定できます[ **! wdfkd.wdfldr** ](-wdfkd-wdfldr.md) "WdfGlobals"フィールドを探します。 または、@@(Driver! を指定できます。WdfDriverGlobals) アドレスの値として、*ドライバー*ドライバーの名前を指定します。 存在する場合*WdfDriverGlobals*アドレスを指定すると、 *DriverName* (ただし、それでも指定する必要があります) は無視されます。
-   UMDF:*HostProcessId* -wudfhost.exe のインスタンスのプロセス ID。 プロセス ID を指定する場合、このコマンドは、そのプロセスのログ レコードを表示します。 プロセス ID を指定しない場合、このコマンドは、次の形式でコマンドの一覧を表示します。

    **!wdflogdump** *DriverName* **** *ProcessID*

    が自動的に選択される、1 つのプロセスを決定できます。 場合、

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
KMDF:

**-d**ドライバー ログのみが表示されます。

**-f**フレームワークのログのみが表示されます。

**-** *LogAddress*特定のドライバーのログが表示されます。 このオプションを使用する場合、LogAddress を指定する必要があります。

UMDF:

**-d**ドライバー ログのみが表示されます。

**-f**フレームワークのログのみが表示されます。

**-m**フレームワークとドライバーのログ記録された順序でマージします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

<a name="remarks"></a>コメント
-------

省略した場合、 *DriverName*パラメーター、既定のドライバー名を使用します。 使用して、 [ **! wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)既定ドライバーの名前を表示して使用する拡張機能、 [ **! wdfkd.wdfsetdriver** ](-wdfkd-wdfsetdriver.md)の拡張機能既定のドライバーの名前を設定します。

フレームワークのエラー ログの記録を表示する、[小さいメモリ ダンプ](small-memory-dump.md)を使用して、 [ **! wdfkd.wdfcrashdump** ](-wdfkd-wdfcrashdump.md)拡張機能。

デバッガーは、WPP トレース メッセージの書式を設定する必要がある情報を設定する方法の詳細については、次を参照してください[ **! wdfkd.wdftmffile** ](-wdfkd-wdftmffile.md)と[ **! wdfkd.wdfsettraceprefix。** ](-wdfkd-wdfsettraceprefix.md).

**追加情報**

実行中のトレース レコーダーには、ドライバーを有効にする方法については、次を参照してください。[を使用して転送トレース レコーダー (IFR) KMDF および UMDF 2 ドライバー](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers)します。 ドライバーを WDF のデバッグの詳細については、次を参照してください。[デバッグ WDF ドライバー](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)します。 KMDF のデバッグ方法の詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ **!wdfkd.wdfcrashdump**](-wdfkd-wdfcrashdump.md)

[ **!wdfkd.wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md)

 

 






