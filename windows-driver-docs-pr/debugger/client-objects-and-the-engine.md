---
title: クライアント オブジェクトとエンジン
description: クライアント オブジェクトとエンジン
ms.assetid: 959912c0-bce9-4d5b-9119-1ac07a8ea1ad
keywords:
- EngExtCpp 拡張機能、クライアントオブジェクト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7ef7dad95b4541eaed2a824aaaf329e1ad88d49
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837825"
---
# <a name="client-objects-and-the-engine"></a>クライアント オブジェクトとエンジン


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


EngExtCpp 拡張機能は、クライアントオブジェクトを介して[デバッガーエンジン](introduction.md#debugger-engine)と対話します。 クライアントオブジェクトへのインターフェイスポインターは、 [**extextension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)基本クラスのメンバーを通じて拡張で使用できます。 次のメンバーは、エンジン API インターフェイスの最初のバージョンへのアクセスを提供します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エンジン API インターフェイス</th>
<th align="left">ExtExtension メンバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced" data-raw-source="[IDebugAdvanced](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced)">IDebugAdvanced</a></p></td>
<td align="left"><p><strong>m_Advanced</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient" data-raw-source="[IDebugClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient)">IDebugClient</a></p></td>
<td align="left"><p><strong>m_Client</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol" data-raw-source="[IDebugControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)">IDebugControl</a></p></td>
<td align="left"><p><strong>m_Control</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces" data-raw-source="[IDebugDataSpaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces)">IDebugDataSpaces</a></p></td>
<td align="left"><p><strong>m_Data</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters" data-raw-source="[IDebugRegisters](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters)">IDebugRegisters</a></p></td>
<td align="left"><p><strong>m_Registers</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols" data-raw-source="[IDebugSymbols](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols)">IDebugSymbols</a></p></td>
<td align="left"><p><strong>m_Symbols</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects" data-raw-source="[IDebugSystemObjects](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects)">IDebugSystemObjects</a></p></td>
<td align="left"><p><strong>m_System</strong></p></td>
</tr>
</tbody>
</table>

 

次のメンバーは、エンジン API インターフェイスの新しいバージョンへのアクセスを提供します。 これらのインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。 使用できない場合、それらを使用しようとすると、例外がスローされます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エンジン API インターフェイス</th>
<th align="left">ExtExtension メンバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IDebugAdvanced2</strong></p></td>
<td align="left"><p><strong>m_Advanced2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugAdvanced3</strong></p></td>
<td align="left"><p><strong>m_Advanced3</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugClient2</strong></p></td>
<td align="left"><p><strong>m_Client2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugClient3</strong></p></td>
<td align="left"><p><strong>m_Client3</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugClient4</strong></p></td>
<td align="left"><p><strong>m_Client4</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugClient5</strong></p></td>
<td align="left"><p><strong>m_Client5</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugControl2</strong></p></td>
<td align="left"><p><strong>m_Control2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugControl3</strong></p></td>
<td align="left"><p><strong>m_Control3</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugControl4</strong></p></td>
<td align="left"><p><strong>m_Control4</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugData2</strong></p></td>
<td align="left"><p><strong>m_Data2</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugData3</strong></p></td>
<td align="left"><p><strong>m_Data3</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugData4</strong></p></td>
<td align="left"><p><strong>m_Data4</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugRegisters2</strong></p></td>
<td align="left"><p><strong>m_Registers2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugSymbols2</strong></p></td>
<td align="left"><p><strong>m_Symbols2</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugSymbols3</strong></p></td>
<td align="left"><p><strong>m_Symbols3</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugSystemObjects2</strong></p></td>
<td align="left"><p><strong>m_System2</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugSystemObjects3</strong></p></td>
<td align="left"><p><strong>m_System3</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugSystemObjects4</strong></p></td>
<td align="left"><p><strong>m_System4</strong></p></td>
</tr>
</tbody>
</table>

 

拡張ライブラリを使用して拡張コマンドを実行したり、出力の構造体をフォーマットしたりするたびに、これらのテーブルのメンバーが初期化されます。 タスクが完了すると、これらのメンバーは初期化されません。 そのため、拡張機能はこれらのメンバーの値をキャッシュしないようにし、 **Extextension**メンバーを直接使用する必要があります。

拡張ライブラリでは、 [**IDebugClient:: createclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createclient)メソッドまたは[**Debugcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugcreate)または[**debugcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)関数を使用して、独自のクライアントオブジェクトを作成することもできます。

クライアントオブジェクトの概要については、「[クライアントオブジェクト](client-objects.md)」を参照してください。

 

 





