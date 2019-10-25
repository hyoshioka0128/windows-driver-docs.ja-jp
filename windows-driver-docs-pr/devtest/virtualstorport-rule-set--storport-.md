---
title: VirtualStorport の規則セット (Storport)
description: これらのルールを使用して、ドライバーが Storport 仮想ミニポート (VMiniport ポート) ドライバーに特に関心のある DDIs を正しく呼び出していることを確認します。
ms.assetid: 7223AFF1-7EB7-4E25-BC50-8A7BF4E4BE59
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: afff2b18536397dcb5ef24869b7f95185df14133
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839985"
---
# <a name="virtualstorport-rule-set-storport"></a>VirtualStorport の規則セット (Storport)


これらのルールを使用して、ドライバーが Storport 仮想ミニポート (VMiniport ポート) ドライバーに特に関心のある DDIs を正しく呼び出していることを確認します。

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
<td align="left"><p><a href="storport-doubleexfreepool.md" data-raw-source="[&lt;strong&gt;DoubleExFreePool&lt;/strong&gt;](storport-doubleexfreepool.md)"><strong>DoubleExFreePool</strong></a></p></td>
<td align="left"><p>このルールは、ドライバーが同じプールメモリブロックを2回解放しようとしないことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-doublekesetevent.md" data-raw-source="[&lt;strong&gt;DoubleKeSetEvent&lt;/strong&gt;](storport-doublekesetevent.md)"><strong>DoubleKeSetEvent</strong></a></p></td>
<td align="left"><p>このルールは、同じイベントオブジェクトで<strong>KeSetEvent</strong>が2回呼び出されていないことを確認します。 同じイベントオブジェクトがルーチンに渡されると、ドライバーはルールに失敗します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-iofreeirp.md" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](storport-iofreeirp.md)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>Ioallocateirp</strong>によって割り当てられた IRP が<strong>Iofreeirp</strong>によって解放されるか、またはその完了ルーチンが<strong>iosetcompletion ルーチン</strong>によって設定されることを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportvirtualdevice.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice&lt;/strong&gt;](storport-storportvirtualdevice.md)"><strong>StorPortVirtualDevice</strong></a></p></td>
<td align="left"><p>このルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>ルーチンが終了したときに、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))"><strong>PORT_CONFIGURATION_INFORMATION (Storport)</strong></a>構造の<strong>virtualdevice</strong>フィールドが<strong>FALSE</strong>に設定されていることを確認します。 このルールは、物理 StorPort ミニポートにのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportvirtualdevice2.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice2&lt;/strong&gt;](storport-storportvirtualdevice2.md)"><strong>StorPortVirtualDevice2</strong></a></p></td>
<td align="left"><p>このルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>ルーチンが終了したときに、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))"><strong>PORT_CONFIGURATION_INFORMATION (Storport)</strong></a>構造の<strong>virtualdevice</strong>フィールドが<strong>TRUE</strong>に設定されていることを確認します。 このルールは、バーチャル StorPort ミニポートにのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](storport-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p>このルールは、通常のカーネル APC 配信が無効になっている場合にのみ、ドライバーの特定の同期機能の呼び出しが行われることを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](storport-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p>このルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)"><strong>ZwCreateKey</strong></a>で作成されたレジストリキーへのハンドルが、その後、他の<em>zwxxx</em>ルーチンによって正しく使用されていることを確認します。 既に開いているハンドルでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)"><strong>Zwopenkey</strong></a>ルーチンを呼び出すことはできません。 ルーチン<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey" data-raw-source="[&lt;strong&gt;ZwEnumerateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)"><strong>ZwEnumerateKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey" data-raw-source="[&lt;strong&gt;ZwEnumerateValueKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey)"><strong>ZwEnumerateValueKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey" data-raw-source="[&lt;strong&gt;ZwFlushKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey)"><strong>zwflushkey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey" data-raw-source="[&lt;strong&gt;ZwQueryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey)"><strong>zwflushkey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey" data-raw-source="[&lt;strong&gt;ZwQueryValueKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)"><strong>zwqueryvaluekey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey" data-raw-source="[&lt;strong&gt;ZwSetValueKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)"><strong>Zwsetvaluekey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>zwclose</strong></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)"><strong>zwflushkey</strong></a>をハンドルで呼び出すことはできませんこれは開いていません。 を返す前に、ハンドルも閉じる必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>Zwopenkey</strong>経由で開かれたレジストリキーへのハンドルが、その後、他の ZwXxx ルーチンによって正しく使用されることを確認します。 ルーチン<strong>ZwEnumerateKey</strong>、 <strong>ZwEnumerateValueKey</strong>、 <strong>zwflushkey</strong>、 <strong>zwflushkey</strong>、 <strong>zwqueryvaluekey</strong>、 <strong>Zwsetvaluekey</strong>、 <strong>zwclose</strong>、および<strong>zwflushkey</strong>を、ではないハンドルで呼び出すことはできません。開き. を返す前に、ハンドルも閉じる必要があります。</p></td>
</tr>
</tbody>
</table>

 

**VirtualStorport ルールセットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[virtualstorport]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**virtualstorport**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:VirtualStorport.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





