---
title: イミディ エイト アイドル タイムアウトのオプトイン
description: このトピックでは、Windows 8 ドライバーのオプトイン状態、電源がすぐに電源が不要になったときに使用できる ImmediateIdle レジストリ値について説明します。
ms.assetid: 43721EC9-4901-4C68-9CCC-E0A71BF2200E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2de1bcac68be13f32c96039adea5e499282f640
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557205"
---
# <a name="span-idaudioimmediateidletimeoutopt-inspanimmediate-idle-timeout-opt-in"></a><span id="audio.immediate_idle_timeout_opt-in"></span>イミディ エイト アイドル タイムアウトのオプトイン


このトピックで説明、 *ImmediateIdle*オプトイン状態、電源がすぐに電力が不要になったときに使用できる Windows 8 ドライバーのレジストリ値。

説明した既定の電源設定だけでなく[PortCls レジストリ電源設定](portcls-registry-power-settings.md)Windows 8 にも、関連するドライバーの PowerSettings レジストリ キーにある新しいレジストリ値が導入されています。 たとえば、キーを持つ、ドライバーがある場合は&lt;UVXYZ&gt;ドライバーの電源設定の情報は、Windows レジストリ内の次のパスで見つかっては。

HKLM\\システム\\CurrentControlSet\\コントロール\\クラス\\{4D36E96C-E325-11CE-BFC1-08002BE10318}\\&lt;UVXYZ&gt; \\PowerSettings します。

出力に表示される値の設定だけでなく、既定および[PortCls レジストリ電源設定](portcls-registry-power-settings.md)、次の行を追加することも、 *ImmediateIdle*:

``` syntax
"ImmediateIdle"=hex:00,00,00,00  
```

*ImmediateIdle* REG のデータ型を持つ\_DWORD とその既定値は「0」を FALSE に相当します。 フラグメントでは、上記の構文、デバイスはすぐの電源の電源が不要になったときに「0」の 16 進数の値。

即時の状態、電源をオプトインするドライバーの電源を不要になったときは、次の構文を使用する必要があります。

``` syntax
"ImmediateIdle"=hex:01,00,00,00  
```

前の構文フラグメントでは、「1」の 16 進値として TRUE を保持し、電源が不要になったときに、デバイスがダウン power すぐにことを意味します。

実行時の電源管理フレームワークがのコールバックを呼び出すときに、 **DevicePowerRequired**メソッド、デバイスが不要になった PortCls の電源が必要ですし、によって示されるD状態のデバイスの電源IRPを要求することを示す*IdlePowerState*レジストリ値。 状態が指定されていない場合は、D3 の既定値が使用されます。

場合、即時のアイドル状態の電源管理に opts ドライバー、連続的に受信したアダプターの Irp の上下に継続的に電源を不必要に防ぐために必要なロジックがシステムの電源エンジン プラグイン (PEP) に含まれています、ことを確認する必要があります。 デバイスの I/O 要求のバッチ用に電源を保持するためにいくつかの保存場所のルールを適用する必要があります。

さらに、ドライバーのプログラムで有効または無効に、アイドル状態の電源管理を許可する Windows 7 で導入された新しいインターフェイスは引き続き、ドライバーがないにオプトイン即時のアイドル状態の電源管理が受け入れられます。 使用してこれには、 [ **IPortClsPower::SetIdlePowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff536875)メソッド場合を除いて、レジストリの設定の上書きが行う*ImmediateIdle*は1 (TRUE) に設定します。

 

 




