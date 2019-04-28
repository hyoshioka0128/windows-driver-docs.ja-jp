---
title: クライアント オブジェクトとエンジン
description: クライアント オブジェクトとエンジン
ms.assetid: 959912c0-bce9-4d5b-9119-1ac07a8ea1ad
keywords:
- クライアント オブジェクト、EngExtCpp 拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f403828220749a4e67121400096d2a18df72ce9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375094"
---
# <a name="client-objects-and-the-engine"></a>クライアント オブジェクトとエンジン


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


EngExtCpp 拡張機能の対話、[デバッガー エンジン](introduction.md#debugger-engine)クライアント オブジェクトを使用します。 クライアント オブジェクトへのインターフェイス ポインターは、拡張機能のメンバーに使用可能な[ **ExtExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff543981)基本クラス。 次のメンバーでは、エンジンの API インターフェイスの最初のバージョンへのアクセスを提供します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549798" data-raw-source="[IDebugAdvanced](https://msdn.microsoft.com/library/windows/hardware/ff549798)">IDebugAdvanced</a></p></td>
<td align="left"><p><strong>m_Advanced</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549827" data-raw-source="[IDebugClient](https://msdn.microsoft.com/library/windows/hardware/ff549827)">IDebugClient</a></p></td>
<td align="left"><p><strong>m_Client</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550508" data-raw-source="[IDebugControl](https://msdn.microsoft.com/library/windows/hardware/ff550508)">IDebugControl</a></p></td>
<td align="left"><p><strong>m_Control</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550528" data-raw-source="[IDebugDataSpaces](https://msdn.microsoft.com/library/windows/hardware/ff550528)">IDebugDataSpaces</a></p></td>
<td align="left"><p><strong>m_Data</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550825" data-raw-source="[IDebugRegisters](https://msdn.microsoft.com/library/windows/hardware/ff550825)">IDebugRegisters</a></p></td>
<td align="left"><p><strong>m_Registers</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550856" data-raw-source="[IDebugSymbols](https://msdn.microsoft.com/library/windows/hardware/ff550856)">IDebugSymbols</a></p></td>
<td align="left"><p><strong>m_Symbols</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550875" data-raw-source="[IDebugSystemObjects](https://msdn.microsoft.com/library/windows/hardware/ff550875)">IDebugSystemObjects</a></p></td>
<td align="left"><p><strong>m_System</strong></p></td>
</tr>
</tbody>
</table>

 

次のメンバーでは、以降のバージョンのエンジンの API インターフェイスへのアクセスを提供します。 これらのインターフェイスは、デバッガー エンジンのすべてのバージョンでできない場合があります。 使用できない場合、それらを使用しようがスローされる例外を発生します。

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

 

これらのテーブル内のメンバーは、拡張機能コマンドまたは形式の出力の構造を実行、拡張機能ライブラリが使用されるたびに初期化されます。 タスクが完了すると、これらのメンバーは初期化されていないが。 その結果、拡張機能はこれらのメンバーの値をキャッシュする必要があり、使用する必要があります、 **ExtExtension**直接のメンバー。

拡張ライブラリは、独自のクライアントのメソッドを使用してオブジェクトを作成もできる[ **IDebugClient::CreateClient** ](https://msdn.microsoft.com/library/windows/hardware/ff539320)または関数[ **DebugCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff540469)または[ **DebugConnect**](https://msdn.microsoft.com/library/windows/hardware/ff540465)します。

クライアント オブジェクトの概要については、次を参照してください。[クライアント オブジェクト](client-objects.md)します。

 

 





