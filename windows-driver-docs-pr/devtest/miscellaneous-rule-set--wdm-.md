---
title: その他の規則セット (WDM)
description: これらの規則を使用すると、ドライバー、正しく一般的な一連のレジストリ キー、文字列とデバイス オブジェクト ポインターの適切な処理の要件に従うことを確認します。
ms.assetid: 50E8BFFE-AC38-4023-9FFB-DC53B749A603
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0cb9e0f4a10983552c1cc75fb58caf91687e37c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361285"
---
# <a name="miscellaneous-rule-set-wdm"></a>その他の規則セット (WDM)


これらの規則を使用すると、ドライバー、正しく一般的な一連のレジストリ キー、文字列とデバイス オブジェクト ポインターの適切な処理の要件に従うことを確認します。

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
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"><strong>AddDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"> <strong>AddDevice</strong> </a>ルールを指定するドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)"> <strong>AddDevice</strong> </a>ルーチンの呼び出し<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)"> <strong>IoAttachDeviceToDeviceStack</strong> </a>呼び出した後のみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)"> <strong>IoCreateDevice</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"><strong>DanglingDeviceObjectReference</strong></a></p></td>
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"> <strong>DanglingDeviceObjectReference</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)"> <strong>ObDereferenceObject</strong> </a>同じデバイスオブジェクトのポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference" data-raw-source="[&lt;strong&gt;IoGetAttachedDeviceReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference)"> <strong>IoGetAttachedDeviceReference</strong> </a>が返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"><strong>PnpSameDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"> <strong>PnpSameDeviceObject</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)"> <strong>IoAttachDeviceToDeviceStack</strong> </a>を有効なポインターを使用ターゲット デバイスのオブジェクト。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"><strong>TargetRelationNeedsRef</strong></a></p></td>
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"> <strong>TargetRelationNeedsRef</strong> </a>ルール指定を処理するときに、 <em>TargetDeviceRelation</em>クエリ、ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchPnP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <strong>DispatchPnP</strong> </a>ルーチンは、子デバイスの PDO を参照するには、次の関数のいずれかを呼び出します。</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)"><strong>ObReferenceObject</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer" data-raw-source="[&lt;strong&gt;ObReferenceObjectByPointer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)"><strong>ObReferenceObjectByPointer</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"> <strong>ZwRegistryCreate</strong> </a>規則の指定後呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)"> <strong>ZwCreateKey</strong></a>ドライバーは、次のレジストリを呼び出すことができますレジストリ キーを開いているハンドルを保持している場合にのみ関数 (つまり、いずれかの呼び出し前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)"> <strong>ZwClose</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey)"> <strong>ZwDeleteKey</strong> </a>終了またはレジストリ キーを識別するハンドルを削除する)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](wdm-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"> <strong>ZwRegistryOpen</strong> </a>規則の指定後呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)"> <strong>ZwOpenKey</strong></a>ドライバーは、次のレジストリ関数のみを呼び出す開いているハンドルをレジストリ キーを押しながら (つまり、呼び出す前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)"> <strong>ZwClose</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey)"> <strong>ZwDeleteKey</strong></a>)。</p></td>
</tr>
</tbody>
</table>

 

**その他のルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **その他**。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Miscellaneous.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





