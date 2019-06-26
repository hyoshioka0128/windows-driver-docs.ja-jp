---
title: Serenum 用のレジストリ設定
description: Serenum 用のレジストリ設定
ms.assetid: c8a8f1b7-ea58-49ed-98e0-40297ec9a769
keywords:
- Serenum ドライバー WDK、レジストリ設定
- レジストリの WDK シリアル デバイス
- シリアル デバイス WDK、レジストリ設定
- シリアル デバイス WDK、Serenum ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44676e967ae4c07deed76d76bbceb06b92ca2ccd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356852"
---
# <a name="registry-settings-for-serenum"></a>Serenum 用のレジストリ設定

このトピックでは、Microsoft Windows 2000 以降の rs-232 ポート Serenum を使用するエントリの値を示します。

次のレジストリ エントリの値では、プラグ アンド プレイ ハードウェア デバイスのレジストリ キー、rs-232 ポートの下です。

<a href="" id="portname--reg-sz-"></a>**PortName** (REG\_SZ)  
ポートの名前を指定します。 Serenum がこの値を読み取りへの応答のポート名を返します、 [ **IOCTL\_SERENUM\_取得\_ポート\_名前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serenum_get_port_name)要求。

<a href="" id="identifier--reg-sz-"></a>**識別子**(REG\_SZ)  
ポートの名前を指定します。 Serenum では、この値を読み取ります。 サポート、**識別子**エントリの値は、一部のレガシ PCMCIA デバイスとの互換性にのみ提供されます。 使用、**識別子**エントリの値は廃止され、Windows 2000 以降のドライバーでは実装されない必要があります。 Serenum IOCTL への応答ポート名を返します\_SERENUM\_取得\_ポート\_名前要求。

<a href="" id="skipenumerations--reg-dword-"></a>**SkipEnumerations** (REG\_DWORD)  
Windows XP 以降では、このエントリの値は Serenum がへの応答のポートを列挙するときを制御する[ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)要求**BusRelations**します。 

たびに、システムは、シリアル ポートのデバイス スタックを構築、Serenum 設定、*列挙モード*ポートを列挙するために使用します。 ポートのデバイス スタックの Serenum の初期化中に[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンでは、ポートの読み取り**SkipEnumerations**エントリの値として列挙モードの設定次の表で説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>列挙モード</th>
<th>SkipEnumerations 値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>通常の列挙します。</p></td>
<td><p>0x00000000</p>
<p>(または値のエントリが存在しない)</p></td>
<td><p>Serenum すべてへの応答でシリアル ポートを列挙する<strong>BusRelations</strong>要求 (ユーザーがデバイス マネージャーまたはハードウェアの追加ウィザードを実行またはシステムのブートによって開始された) かどうか。</p></td>
</tr>
<tr class="even">
<td><p>指定された列挙数をスキップします。</p></td>
<td><p>0xFFFFFFE 0x00000001 からの値</p></td>
<td><p>Serenum は列挙型の指定した数をスキップし、その後、ポートが有効になっている限り、通常を列挙します。</p></td>
</tr>
<tr class="odd">
<td><p>すべての列挙体をスキップします。</p></td>
<td><p>0 xffffffff</p></td>
<td><p>Serenum しないポートを列挙します。 ポートに接続されたデバイスを手動でインストールする必要があります。</p></td>
</tr>
</tbody>
</table>

たとえば、シリアル ポートの**SkipEnumerations**システムは、ポートのデバイス スタックを作成するときに、エントリの値が 3 に設定されて、Serenum は最初の 3 つをスキップ**BusRelations**ポートの受信要求。 ポートが有効になっている限り Serenum は通常の方法で、その後、ポートを列挙します。
