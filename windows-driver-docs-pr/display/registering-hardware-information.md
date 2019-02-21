---
title: ハードウェア情報を登録します。
description: ハードウェア情報を登録します。
ms.assetid: 1fec9fcf-3ec7-4926-9ceb-ef1f7f42e963
keywords:
- レジストリ WDK の表示
- レジストリの WDK 表示でハードウェアの情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca8910e3aafbbc0532a6694a9f7db9ea3405cd00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530170"
---
# <a name="registering-hardware-information"></a>ハードウェア情報を登録します。


ユーザーとデバッグについての支援を有用な情報を表示するには、ディスプレイのミニポート ドライバーは、レジストリの特定のハードウェア情報を設定する必要があります。 ディスプレイのミニポート ドライバーには、チップの種類、アナログ デジタル コンバーター (DAC) 型、(アダプター) のメモリ サイズおよびアダプターを識別する文字列を設定する必要があります。 この情報で表示されます、**表示**コントロール パネルの アプリケーション。 通常、ドライバーがこの情報を設定その[ **DxgkDdiAddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff559586)関数。

この情報は、ドライバーを設定するには。

1.  呼び出し、 **IoOpenDeviceRegistryKey**ドライバー固有の情報を格納するためです。 この呼び出しで、ドライバーは、PLUGPLAY を指定します\_REGKEY\_ドライバー フラグ、 *DevInstKeyType*パラメーターと、キー\_設定\_値、キー\_書き込み、またはキー\_すべて\_アクセス値で、 *DesiredAccess*パラメーター。

2.  呼び出し、 [ **ZwSetValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567109)ハードウェア情報の種類ごとの設定を複数回に機能します。 各呼び出しで、ドライバー単位で指定します、 *KeyHandle*パラメーターでは、ソフトウェア キー ハンドルから取得された**IoOpenDeviceRegistryKey**します。

    次の表に、ドライバーを選択し、登録する必要がありますの詳細を提供情報、 *ValueName*と*データ*パラメーターの**ZwSetValueKey**:

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
    <td align="left"><p>HardwareInformation.ChipType</p></td>
    <td align="left"><p>チップの名前を含む null で終わる文字列</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DAC 型</p></td>
    <td align="left"><p>HardwareInformation.DacType</p></td>
    <td align="left"><p>DAC の名前または識別子 (ID) を含む null で終わる文字列</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>メモリ サイズ</p></td>
    <td align="left"><p>HardwareInformation.MemorySize</p></td>
    <td align="left"><p>アダプターのビデオ メモリの量をメガバイト単位で含まれている ULONG</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>アダプター ID</p></td>
    <td align="left"><p>HardwareInformation.AdapterString</p></td>
    <td align="left"><p>アダプターの名前を含む null で終わる文字列</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>BIOS</p></td>
    <td align="left"><p>HardwareInformation.BiosString</p></td>
    <td align="left"><p>BIOS に関する情報を含む null で終わる文字列</p></td>
    </tr>
    </tbody>
    </table>

     

 

 





