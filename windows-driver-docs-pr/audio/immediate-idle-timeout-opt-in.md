---
title: 即時アイドル タイムアウトのオプトイン
description: このトピックでは、電源が不要になったときに、Windows 8 ドライバーが即座に電源をオンにするために使用できる ImmediateIdle レジストリ値について説明します。
ms.assetid: 43721EC9-4901-4C68-9CCC-E0A71BF2200E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020b439b78502ac87841d8062810cf9aed9dad26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833279"
---
# <a name="span-idaudioimmediate_idle_timeout_opt-inspanimmediate-idle-timeout-opt-in"></a><span id="audio.immediate_idle_timeout_opt-in"></span>即時アイドルタイムアウトオプトイン


このトピックでは、電源が不要になったときに、Windows 8 ドライバーが即座に電源をオンにするために使用できる*ImmediateIdle*レジストリ値について説明します。

「 [PortCls Registry の電源設定](portcls-registry-power-settings.md)」で説明されている既定の電源設定に加えて、Windows 8 では、関連付けられているドライバーの powersettings レジストリキーにもある新しいレジストリ値が導入されています。 たとえば、キーが UVXYZ&gt;&lt;されているドライバーがある場合、ドライバーの電源設定情報は Windows レジストリの次のパスにあります。

HKLM\\System\\CurrentControlSet\\Control\\クラス\\{4D36E96C-E325-11CE-BFC1-08002BE10318}\\&lt;UVXYZ&gt;\\PowerSettings。

また、 [PortCls レジストリの [電源設定](portcls-registry-power-settings.md)] に表示される既定の電源設定値に加えて、 *ImmediateIdle*には次の行も含まれます。

``` syntax
"ImmediateIdle"=hex:00,00,00,00  
```

*ImmediateIdle*のデータ型は REG\_DWORD で、既定値は "0" で、FALSE になります。 上記の構文フラグメントでは、16進値 "0" は、電力が不要になったときにデバイスの電源がすぐに切断されないことを意味します。

ドライバーが即座に電源を切る状態にするには、電源が不要になったら、次の構文を使用する必要があります。

``` syntax
"ImmediateIdle"=hex:01,00,00,00  
```

上記の構文フラグメントでは、16進値 "1" は TRUE に相当します。これは、電源が不要になったときに、デバイスの電源がすぐに切断されることを意味します。

ランタイム電源管理フレームワークが**Devicepowerrequired**メソッドのコールバックを呼び出し、デバイスが電力を必要としないことを示している場合、PortCls は、 *IdlePowerState*によって示された D 状態のデバイス電源 IRP を要求します。レジストリ値。 状態が指定されていない場合は、D3 の既定値が使用されます。

ドライバーが即時アイドル電源管理を使用する場合は、システムの電源エンジンプラグイン (PEP) に、不必要に受信した Irp に対してアダプターを上下に継続的に電源投入するために必要なロジックが含まれていることを確認する必要があります。 I/o 要求のバッチに対してデバイスの電源を入れたままにするために、いくつかの常駐ルールを適用する必要があります。

さらに、Windows 7 で導入された新しいインターフェイスでは、ドライバーがプログラムによってアイドル電源管理を有効または無効にすることができます。これは、ドライバーが即時アイドル電源管理にオプトインしていない場合でも引き続き受け入れられます。 これは[**IPortClsPower:: SetIdlePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspower-setidlepowermanagement)メソッドを使用して実行され、 *ImmediateIdle*が 1 (TRUE) に設定されている場合を除き、レジストリの設定をオーバーライドします。

 

 




