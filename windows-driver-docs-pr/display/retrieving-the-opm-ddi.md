---
title: OPM DDI の取得
description: OPM DDI の取得
ms.assetid: 84218245-f5f3-4a6f-88ed-9cd5db224e30
keywords:
- OPM WDK の表示、DDI を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb2139eaff2193ef52ff07870eb80750321674e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365657"
---
# <a name="retrieving-the-opm-ddi"></a>OPM DDI の取得


次の順序は、Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) を表示ミニポート ドライバーを取得する方法を示しています[OPM DDI](supporting-output-protection-manager.md):。

1. DirectX グラフィックスのカーネル サブシステム呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiAddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_add_device)グラフィックス アダプターのコンテキストのブロックを作成して、そのグラフィックス アダプターにハンドルを返す関数。

2. DirectX グラフィックスのカーネルのサブシステムを初期化します、 [**クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_query_interface)次の表の値を持つ構造体。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">メンバー名</th>
   <th align="left">メンバーの種類</th>
   <th align="left">Value</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceType</strong></p></td>
   <td align="left"><p>CONST PGUID</p></td>
   <td align="left"><p>GUID_DEVINTERFACE_OPM へのポインター</p>
   <p>(BF4672DE-6B4E-4BE4-A325-68A91EA49C09)</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>サイズ</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>sizeof(DXGK_OPM_INTERFACE)</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>バージョン</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>DXGK_OPM_INTERFACE_VERSION_1</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>Interface</strong></p></td>
   <td align="left"><p>PINTERFACE</p></td>
   <td align="left"><p>ポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_opm_interface" data-raw-source="[&lt;strong&gt;DXGK_OPM_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_opm_interface)"> <strong>DXGK_OPM_INTERFACE</strong> </a>構造体</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceSpecificData</strong></p></td>
   <td align="left"><p>PVOID</p></td>
   <td align="left"><p>NULL</p></td>
   </tr>
   </tbody>
   </table>

     

3. DirectX グラフィックスのカーネル サブシステムが初期化されたクエリを渡す\_ディスプレイ ミニポート ドライバーの呼び出しでインターフェイス[ **DxgkDdiQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数。

4. ディスプレイのミニポート ドライバーが、OPM インターフェイスをサポートしていない場合[ **DxgkDdiQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)状態を返す必要があります\_いない\_サポートされています。

   ディスプレイのミニポート ドライバー OPM をサポートしている場合[ **DxgkDdiQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)を初期化します、 [ **DXGK\_OPM\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_opm_interface)で受信した構造体、**インターフェイス**のメンバー [**クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_query_interface)で値を持つ、次の表にします。

   **メンバーの名前、種類、および値:**

   <span id="Size"></span><span id="size"></span><span id="SIZE"></span>**サイズ**  
   USHORT 型

   sizeof (DXGK\_OPM\_インターフェイス)

   <span id="Version"></span><span id="version"></span><span id="VERSION"></span>**バージョン**  
   USHORT 型

   DXGK\_OPM\_インターフェイス\_バージョン\_1

   <span id="InterfaceReference"></span><span id="interfacereference"></span><span id="INTERFACEREFERENCE"></span>**InterfaceReference**  
   入力 PINTERFACE\_リファレンス

   ディスプレイのミニポート ドライバーへのポインター **InterfaceReference**ルーチン (について**InterfaceReference**の「解説」を参照してください、 [**インターフェイス** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)構造です)。

   <span id="InterfaceDereference"></span><span id="interfacedereference"></span><span id="INTERFACEDEREFERENCE"></span>**InterfaceDereference**  
   入力 PINTERFACE\_逆参照

   ディスプレイのミニポート ドライバーへのポインター **InterfaceDereference**ルーチン (について**InterfaceDereference**の「解説」を参照してください、 [**インターフェイス** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)構造です)。

   <span id="DxgkDdiOPMGetCertificateSize"></span><span id="dxgkddiopmgetcertificatesize"></span><span id="DXGKDDIOPMGETCERTIFICATESIZE"></span>**DxgkDdiOPMGetCertificateSize**  
   入力 DXGKDDI\_OPM\_取得\_証明書\_サイズ

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetCertificateSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)関数

   <span id="DxgkDdiOPMGetCertificate"></span><span id="dxgkddiopmgetcertificate"></span><span id="DXGKDDIOPMGETCERTIFICATE"></span>**DxgkDdiOPMGetCertificate**  
   入力 DXGKDDI\_OPM\_取得\_証明書

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetCertificate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)関数

   <span id="DxgkDdiOPMCreateProtectedOutput"></span><span id="dxgkddiopmcreateprotectedoutput"></span><span id="DXGKDDIOPMCREATEPROTECTEDOUTPUT"></span>**DxgkDdiOPMCreateProtectedOutput**  
   入力 DXGKDDI\_OPM\_作成\_PROTECTED\_出力

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMCreateProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)関数

   <span id="DxgkDdiOPMGetRandomNumber"></span><span id="dxgkddiopmgetrandomnumber"></span><span id="DXGKDDIOPMGETRANDOMNUMBER"></span>**DxgkDdiOPMGetRandomNumber**  
   入力 DXGKDDI\_OPM\_取得\_ランダム\_数

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetRandomNumber** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)関数

   <span id="DxgkDdiOPMSetSigningKeyAndSequenceNumbers"></span><span id="dxgkddiopmsetsigningkeyandsequencenumbers"></span><span id="DXGKDDIOPMSETSIGNINGKEYANDSEQUENCENUMBERS"></span>**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**  
   DXGKDDI\_OPM\_設定\_署名\_キー\_AND\_シーケンス\_番号

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMSetSigningKeyAndSequenceNumbers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)関数

   <span id="DxgkDdiOPMGetInformation"></span><span id="dxgkddiopmgetinformation"></span><span id="DXGKDDIOPMGETINFORMATION"></span>**DxgkDdiOPMGetInformation**  
   DXGKDDI\_OPM\_取得\_情報

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)関数

   <span id="DxgkDdiOPMGetCOPPCompatibleInformation"></span><span id="dxgkddiopmgetcoppcompatibleinformation"></span><span id="DXGKDDIOPMGETCOPPCOMPATIBLEINFORMATION"></span>**DxgkDdiOPMGetCOPPCompatibleInformation**  
   DXGKDDI\_OPM\_取得\_COPP\_互換性のある\_情報

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)関数

   <span id="DxgkDdiOPMConfigureProtectedOutput"></span><span id="dxgkddiopmconfigureprotectedoutput"></span><span id="DXGKDDIOPMCONFIGUREPROTECTEDOUTPUT"></span>**DxgkDdiOPMConfigureProtectedOutput**  
   DXGKDDI\_OPM\_構成\_PROTECTED\_出力

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数

   <span id="DxgkDdiOPMDestroyProtectedOutput"></span><span id="dxgkddiopmdestroyprotectedoutput"></span><span id="DXGKDDIOPMDESTROYPROTECTEDOUTPUT"></span>**DxgkDdiOPMDestroyProtectedOutput**  
   DXGKDDI\_OPM\_破棄\_PROTECTED\_出力

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMDestroyProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)関数

5. ディスプレイのミニポート ドライバーが完了すると、ドライバーの呼び出しである OPM インターフェイスを使用してその**InterfaceDereference**ルーチン。 ドライバーを呼び出す必要があります**InterfaceDereference**する前にその[ **DxgkDdiRemoveDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_remove_device)関数が呼び出されます。

 

 





