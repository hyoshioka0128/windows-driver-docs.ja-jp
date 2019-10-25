---
title: ハードウェア情報の登録
description: ハードウェア情報の登録
ms.assetid: 1fec9fcf-3ec7-4926-9ceb-ef1f7f42e963
keywords:
- レジストリ WDK 表示
- レジストリ WDK 表示のハードウェア情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e1243c267de96605b8f6dbdaec2cb6e290b5c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829635"
---
# <a name="registering-hardware-information"></a>ハードウェア情報の登録


役に立つ情報をユーザーに表示し、デバッグの支援を受けるには、表示ミニポートドライバーでレジストリに特定のハードウェア情報を設定する必要があります。 ディスプレイミニポートドライバーでは、チップの種類、デジタル-アナログコンバーター (DAC) の種類、メモリサイズ (アダプター)、およびアダプターを識別する文字列を設定する必要があります。 この情報は、コントロールパネルの **[表示]** アプリケーションで表示されます。 通常、ドライバーは[**DxgkDdiAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)関数でこの情報を設定します。

この情報を設定するために、ドライバーは次のようになります。

1.  ドライバー固有の情報を格納するために**IoOpenDeviceRegistryKey**を呼び出します。 この呼び出しでは、ドライバーは*Devinstkeytype*パラメーターに PLUGPLAY\_REGKEY\_driver フラグを指定し、キー\_\_値、キー\_書き込み、またはキー\_すべての\_アクセス値に設定します。パラメーター。

2.  [**Zwsetvaluekey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)関数を複数回呼び出して、ハードウェア情報の種類を設定します。 各呼び出しで、ドライバーは**IoOpenDeviceRegistryKey**から取得したソフトウェアキーハンドルを*keyhandle*パラメーターに指定します。

    次の表では、ドライバーが登録する必要がある情報と、 **Zwsetvaluekey**の*ValueName*と*データ*パラメーターの詳細について説明します。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">エントリの情報</th>
    <th align="left"><em>ValueName</em>パラメーター</th>
    <th align="left"><em>データ</em>パラメーター</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>チップの種類</p></td>
    <td align="left"><p>ChipType</p></td>
    <td align="left"><p>チップ名を含む Null で終わる文字列</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DAC 型</p></td>
    <td align="left"><p>ハードウェア情報 DacType</p></td>
    <td align="left"><p>DAC の名前または識別子 (ID) を含む Null で終わる文字列</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>メモリサイズ</p></td>
    <td align="left"><p>ハードウェア情報. MemorySize</p></td>
    <td align="left"><p>アダプターのビデオメモリの量を mb 単位で含む ULONG</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>アダプター ID</p></td>
    <td align="left"><p>ハードウェア情報. AdapterString</p></td>
    <td align="left"><p>アダプターの名前を含む Null で終わる文字列</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>BIOS</p></td>
    <td align="left"><p>ハードウェア情報 (BiosString)</p></td>
    <td align="left"><p>BIOS に関する情報を含む Null で終わる文字列</p></td>
    </tr>
    </tbody>
    </table>

     

 

 





