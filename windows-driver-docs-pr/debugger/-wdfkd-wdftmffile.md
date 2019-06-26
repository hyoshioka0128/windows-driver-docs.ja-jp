---
title: wdfkd.wdftmffile
description: Wdfkd.wdftmffile 拡張機能は、デバッガーが wdfkd.wdflogdump または wdfkd.wdfcrashdump KMDF エラー ログを書式設定時に使用するトレース メッセージの形式 (.tmf) ファイルを設定します。
ms.assetid: 7099440c-bfea-472f-b9ee-943026afdb81
keywords:
- デバッグ wdfkd.wdftmffile Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftmffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 43e964b5f53a774e8e573443cc6d479e5e79a7b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363088"
---
# <a name="wdfkdwdftmffile"></a>!wdfkd.wdftmffile


**! Wdfkd.wdftmffile**拡張機能の設定、デバッガーがカーネル モード ドライバー フレームワーク (KMDF) のエラー ログの記録を書式設定時に使用するトレース メッセージの形式 (.tmf) ファイル、 [ **! wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md)または[ **! wdfkd.wdfcrashdump** ](-wdfkd-wdfcrashdump.md)拡張機能。

```dbgcmd
!wdfkd.wdftmffile TMFpath
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______TMFpath______"></span><span id="_______tmfpath______"></span><span id="_______TMFPATH______"></span> *TMFpath*   
.Tmf ファイルを含むパスです。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

使用する必要があります、ドライバーは、1.11 より前、KMDF バージョンを使用する場合、 **! wdfkd.wdftmffile**拡張機能を使用する前に、 [ **! wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md)または[ **! wdfkd.wdfcrashdump** ](-wdfkd-wdfcrashdump.md)拡張機能。

KMDF バージョン 1.11 以降、フレームワーク ライブラリのシンボル ファイル (たとえば wdf01000.pdb) には、トレース メッセージの形式 (TMF) エントリが含まれています。 以降、カーネル デバッガーの Windows 8 バージョンでは、[カーネル モード ドライバー フレームワークの拡張機能 (Wdfkd.dll)](kernel-mode-driver-framework-extensions--wdfkd-dll-.md) .pdb ファイルからエントリを読み取る。 その結果、KMDF バージョン 1.11 以降を使用するには、ドライバー、Windows 8 またはそれ以降、カーネル デバッガーを使用している場合は、必要はありませんを使用する **! wdfkd.wdftmffile**します。 デバッガーのシンボル ファイルを含むディレクトリを含める必要がある操作を行います[シンボル パス](symbol-path.md)します。 デバッグの対象コンピューターには、KMDF をサポートする任意のオペレーティング システムを実行できます。

次の例は、使用する方法を示します、 **! wdfkd.wdftmffile** kmdf バージョン 1.5 をルート WDK ディレクトリから拡張機能。

```dbgcmd
kd> !wdftmffile tools\tracing\<platform>\wdf1005.tmf
```

別のバージョンで使用している Windows Driver Kit (WDK) のパスである可能性がありますに注意してください。 また、.tmf ファイルの名前が使用している KMDF のバージョンを表すことに注意してください。 たとえば、Wdf1005.tmf、kmdf バージョン 1.5 .tmf ファイルです。

デバッグ セッション中に、KMDF ログを表示する方法については、次を参照してください。[フレームワークのイベントのロガーを使用して](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-s-event-logger)します。

 

 





