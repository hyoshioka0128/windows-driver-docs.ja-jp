---
title: Serenum 用のレジストリ設定
description: Serenum 用のレジストリ設定
ms.assetid: c8a8f1b7-ea58-49ed-98e0-40297ec9a769
keywords:
- Serenum.sys ドライバー WDK、レジストリ設定
- レジストリ WDK シリアルデバイス
- シリアルデバイス WDK、レジストリ設定
- シリアルデバイス WDK、Serenum.sys ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02f1ddb8b77e147a44b49c8e9f9afc0c3f66f61c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844943"
---
# <a name="registry-settings-for-serenum"></a>Serenum 用のレジストリ設定

このトピックでは、Microsoft Windows 2000 以降の RS-232 ポートに対して、Serenum.sys が使用するエントリ値について説明します。

次のレジストリエントリの値は、RS-232 ポートのプラグアンドプレイハードウェアデバイスのレジストリキーの下にあります。

<a href="" id="portname--reg-sz-"></a>**PortName** (REG\_SZ)  
ポートの名前を指定します。 この値を読み取って、IOCTL\_SERENUM.SYS に応答してポート名を返し、 [ **\_ポート\_名前要求を取得\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serenum_get_port_name)ます。

<a href="" id="identifier--reg-sz-"></a>**識別子**(REG\_SZ)  
ポートの名前を指定します。 この値は、serenum.sys によって読み取られます。 **識別子**エントリ値のサポートは、一部のレガシ PCMCIA デバイスとの互換性のためだけに提供されています。 **識別子**エントリ値の使用は廃止されており、Windows 2000 以降のドライバーでは実装しないでください。 Serenum.sys は、IOCTL\_SERENUM.SYS に応答してポート名を返し、\_ポート\_名前要求\_取得します。

<a href="" id="skipenumerations--reg-dword-"></a>**Skipenumerations 型**(REG\_DWORD)  
Windows XP 以降では、このエントリ値は、 **Busrelations**に対する[ **\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)要求に対する IRP\_に応答して、serenum.sys がポートを列挙するタイミングを制御します。 

システムがシリアルポートのデバイススタックを構築するたびに、Serenum.sys はポートを列挙するために使用する*列挙モード*を設定します。 ポートのデバイススタックの初期化中に、Serenum.sys の[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンは、次の表に示すように、ポートの**skipenumerations**エントリ値を読み取り、列挙モードを設定します。

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
<td><p>通常どおりに列挙します。</p></td>
<td><p>―</p>
<p>(または値のエントリが存在しません)</p></td>
<td><p>Serenum.sys は、すべての<strong>Busrelations</strong>要求に応答してシリアルポートを列挙します (システムブートによって開始されたか、ユーザーがデバイスマネージャーまたはハードウェアの追加ウィザードを使用して開始したかどうか)。</p></td>
</tr>
<tr class="even">
<td><p>指定された数の列挙をスキップします。</p></td>
<td><p>0x00000001 から0xFFFFFFE の値</p></td>
<td><p>指定された数の列挙をスキップし、その後、ポートが有効のままであれば通常どおりに列挙します。</p></td>
</tr>
<tr class="odd">
<td><p>すべての列挙をスキップします。</p></td>
<td><p>~</p></td>
<td><p>Serenum.sys はポートを列挙しません。 ポートに接続されているデバイスは、手動でインストールする必要があります。</p></td>
</tr>
</tbody>
</table>

たとえば、システムがポートデバイススタックを構築するときにシリアルポートの**Skipenumerations**エントリ値が3に設定されている場合、serenum.sys はポートに対して受信した最初の3つの**busrelations**要求をスキップします。 その後、ポートが有効になっている限り、serenum.sys は通常の方法でポートを列挙します。
