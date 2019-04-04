---
title: IrpProcessing の規則セット (KMDF)
description: これらの規則を使用すると、ドライバーが I/O 要求パケット (IRP) を正しく処理することを確認します。
ms.assetid: B403F21E-FE35-4A57-92DB-C78FDC1488BD
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 88d1558914e06d08435645db2d088b4889518cc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573719"
---
# <a name="irpprocessing-rule-set-kmdf"></a>IrpProcessing の規則セット (KMDF)


これらの規則を使用すると、ドライバーが I/O 要求パケット (IRP) を正しく処理することを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"><strong>FwdIrpToIoQueueValid</strong></a></p></td>
<td align="left"><p>ルール<a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"> <strong>FwdIrpToIoQueueValid</strong> </a> 、I/O をドライバーが IRP を送信することを指定しますキューを使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh451105" data-raw-source="[&lt;strong&gt;WdfDeviceWdmDispatchIrpToIoQueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451105)"> <strong>WdfDeviceWdmDispatchIrpToIoQueue</strong> </a>。からいずれかのメソッド、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh406404" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406404)"> <em>EvtDeviceWdmIrpDispatch</em> </a>コールバックまたは<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess</em> </a>コールバック。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"><strong>SetCompletionRoutineFromDispatch</strong></a></p></td>
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"> <strong>SetCompletionRoutineFromDispatch</strong> </a>ルールから IRP の完了のルーチンは、ドライバーによって指定されていないことを確認しますその<a href="https://msdn.microsoft.com/library/windows/hardware/hh406404" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406404)"> <em>EvtDeviceWdmIrpDispatch。</em></a>コールバック関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"><strong>MiniportOnlyWdmDevice</strong></a></p></td>
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"> <strong>MiniportOnlyWdmDevice</strong> </a>ルールでは、WDF のドライバーを使用する必要がありますいないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548397" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548397)"> <strong>IoCreateDevice</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff548407" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548407)"> <strong>IoCreateDeviceSecure</strong> </a>ベア WDM デバイス オブジェクトを作成する関数。 これにより、クラッシュを IRP を WDM デバイスに送信するコンピューター。 デバイスの IRP ディスパッチ エントリは、WDF に固有のエントリに設定されますが、フレームワークは、WDF デバイスを作成していないためにです。 ただし、それらのドライバーのディスパッチのエントリ ポイントが設定されていないため、ミニポート ドライバーでは、Ddi を使用できます。</p></td>
</tr>
</tbody>
</table>

 

**IrpProcessing ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **IrpProcessing**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **IrpProcessing.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 





