---
title: イベントのトレース
description: I²C 上、HID で操作をトレースには、Event Tracing for Windows (ETW) または Windows ソフトウェア トレース プリプロセッサ (WPP) を使用できます。
ms.assetid: F23E5516-36B9-478E-90D3-54D1C52CB467
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 970b20c211b3ac163136e14ab5e03d6d843d6cf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557636"
---
# <a name="event-tracing"></a>イベントのトレース


I²C デバイス ドライバー、HID で、操作をトレースするのには、Event Tracing for Windows (ETW) または Windows ソフトウェア トレース プリプロセッサ (WPP) を使用できます。 ETW の詳細については、次を参照してください。、[イベント トレーシング](https://go.microsoft.com/fwlink/p/?linkid=256040)、Windows 開発のリファレンス トピック。 WPP の詳細については、次を参照してください。 [WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)と[ログ トレースのように、転送トレース レコーダー (IFR)](https://msdn.microsoft.com/library/windows/hardware/dn914610)します。

## <a name="using-the-inflight-trace-recorder-ifr"></a>転送トレース レコーダー (IFR) を使用します。


転送トレース レコーダー (IFR)、すべてのドライバーの既定で有効になっているでは、カーネル デバッガーに HIDI²C ドライバーからのトレース出力を表示できます。 次のコマンドでは、HIDI²C の WPP トレース メッセージが表示されます。

``` syntax
!rcdrkd.rcdrlogdump hidi2c
```

転送トレース レコーダー (IFR) は、固定サイズの循環バッファにこれらのトレース メッセージを格納します。 その結果、出力は、全体のトレース ログを含めることはできません。

## <a name="using-logmanexe"></a>Logman.exe を使用してください。


使用することができますより詳細で制御可能なトレースの[logman.exe]( https://go.microsoft.com/fwlink/p/?linkid=256232)トレースをキャプチャします。 次のコマンドの HIDI²C WPP トレースをキャプチャします。

``` syntax
Logman create trace -n HIDI2C_WPP -o HIDI2C_WPP.etl -nb 128 640 -bs 128 
Logman update trace -n HIDI2C_WPP -p {E742C27D-29B1-4E4B-94EE-074D3AD72836} 0x7FFFFFFF 255
Logman start –n HIDI2C_WPP
 
<RUN your SCENARIO here>

Logman stop -n HIDI2C_WPP
Logman delete -n HIDI2C_WPP
```

HIDI²C の PDB または TMF のいずれかのファイルを使用してテキストには、結果のトレース ログ ファイルを解析できます。

## <a name="enabling-etw-tracing"></a>ETW トレースを有効にします。


HIDI²C ドライバーでは、特定のイベントの ETW イベントを記録します。 これらのイベントは、イベント ビューアー ログに記録されます。

次の logman.exe コマンドを使用してこれらのイベントを表示することもできます。

``` syntax
Logman create trace -n HIDI2C_ETW -o HIDI2C_ETW.etl -nb 128 640 -bs 128 
Logman update trace -n HIDI2C_ETW -p Microsoft-Windows-SPB-HIDI2C 
Logman start –n HIDI2C_ETW
 
<RUN your SCENARIO here>

Logman stop -n HIDI2C_ETW
Logman delete -n HIDI2C_ETW
```

などのツールによる結果のトレース ログが解析できる**Xperf**または**Windows Performance Analyzer** (WPA)。

 

 




