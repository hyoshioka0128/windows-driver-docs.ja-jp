---
title: その他の規則セット (KMDF)
description: これらの規則には、ドライバー正しく一般的な一連のデバイスの適切な処理の要件に従うことを確認するオブジェクトの場合、キー、および、ドライバーは Ddi いないは呼び出しが非 PnP ドライバーまたは po ではない非 FDO ドライバーは適切でない使用wer ポリシーの所有者です。
ms.assetid: B8F9FBE1-ED27-47EC-ACFC-8BD354A5E72D
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 14ec67b8e46ea7e7d8676a0c8e79499df0222fbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577911"
---
# <a name="miscellaneous-rule-set-kmdf"></a>その他の規則セット (KMDF)


これらの規則には、ドライバー正しく一般的な一連のデバイスの適切な処理の要件に従うことを確認するオブジェクトの場合、キー、および、ドライバーは Ddi いないは呼び出しが非 PnP ドライバーまたは po ではない非 FDO ドライバーは適切でない使用wer ポリシーの所有者です。

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
<td align="left"><p><a href="kmdf-accesshardwarekey.md" data-raw-source="[&lt;strong&gt;AccessHardwareKey&lt;/strong&gt;](kmdf-accesshardwarekey.md)"><strong>AccessHardwareKey</strong></a></p></td>
<td align="left"><p><a href="kmdf-accesshardwarekey.md" data-raw-source="[&lt;strong&gt;AccessHardwareKey&lt;/strong&gt;](kmdf-accesshardwarekey.md)"> <strong>AccessHardwareKey</strong> </a>ルールは、バス ドライバーしようとしないでくださいから子デバイスのハードウェア キーへのアクセスを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff540828" data-raw-source="[&lt;em&gt;EvtChildListCreateDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540828)"> <em>EvtChildListCreateDevice</em></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-addpdotostaticchildlist.md" data-raw-source="[&lt;strong&gt;AddPdotoStaticChildlist&lt;/strong&gt;](kmdf-addpdotostaticchildlist.md)"><strong>AddPdotoStaticChildlist</strong></a></p></td>
<td align="left"><p>PDO デバイスの場合、framework 関数 AddPdotoStaticChildlist ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff547225" data-raw-source="[&lt;strong&gt;WdfFdoAddStaticChild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547225)"> <strong>WdfFdoAddStaticChild</strong> </a>ドライバー呼び出しの後に呼び出す必要がある<a href="https://msdn.microsoft.com/library/windows/hardware/ff548786" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548786)"> <strong>WdfPdoInitAllocate</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>正常にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-childlistconfiguration.md" data-raw-source="[&lt;strong&gt;ChildListConfiguration&lt;/strong&gt;](kmdf-childlistconfiguration.md)"><strong>ChildListConfiguration</strong></a></p></td>
<td align="left"><p><a href="kmdf-childlistconfiguration.md" data-raw-source="[&lt;strong&gt;ChildListConfiguration&lt;/strong&gt;](kmdf-childlistconfiguration.md)"> <strong>ChildListConfiguration</strong> </a>ルールを指定するドライバーをサポートする<a href="https://msdn.microsoft.com/library/windows/hardware/ff540812" data-raw-source="[Dynamic Enumeration](https://msdn.microsoft.com/library/windows/hardware/ff540812)">動的列挙</a>呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff547258" data-raw-source="[&lt;strong&gt;WdfFdoInitSetDefaultChildListConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547258)"> <strong>WdfFdoInitSetDefaultChildListConfig</strong> </a>呼び出す前に、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-cleanup4ctldeviceregistered.md" data-raw-source="[&lt;strong&gt;Cleanup4CtlDeviceRegistered&lt;/strong&gt;](kmdf-cleanup4ctldeviceregistered.md)"><strong>Cleanup4CtlDeviceRegistered</strong></a></p></td>
<td align="left"><p><a href="kmdf-cleanup4ctldeviceregistered.md" data-raw-source="[&lt;strong&gt;Cleanup4CtlDeviceRegistered&lt;/strong&gt;](kmdf-cleanup4ctldeviceregistered.md)"> <strong>Cleanup4CtlDeviceRegistered</strong> </a>ルールを指定するプラグ アンド プレイ (PnP) ドライバーを呼び出す場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>用、コントロールのデバイス オブジェクト、ドライバーが必要なイベントのコールバック関数のいずれかに登録する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-nonfdonotpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonFDONotPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonfdonotpowerpolicyownerapi.md)"><strong>NonFDONotPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-nonfdonotpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonFDONotPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonfdonotpowerpolicyownerapi.md)"> <strong>NonFDONotPowerPolicyOwnerAPI</strong> </a>ルール FDO 以外のドライバーが電源ポリシーの所有者でない場合は、特定 Ddi できません呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-nonpnpdrvpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonPnPDrvPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonpnpdrvpowerpolicyownerapi.md)"><strong>NonPnPDrvPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-nonpnpdrvpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonPnPDrvPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonpnpdrvpowerpolicyownerapi.md)"> <strong>NonPnPDrvPowerPolicyOwnerAPI</strong> </a>ルールでは、非 PnP ドライバーが電源管理に関連する特定の Ddi を呼び出すことはできませんを指定します。</p></td>
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

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





