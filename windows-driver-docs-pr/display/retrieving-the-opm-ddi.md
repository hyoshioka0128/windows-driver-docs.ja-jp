---
title: OPM DDI の取得
description: OPM DDI の取得
ms.assetid: 84218245-f5f3-4a6f-88ed-9cd5db224e30
keywords:
- OPM WDK 表示、DDI の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31b3f6765429a5bd2db929aa3aef01e9b4e783dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825838"
---
# <a name="retrieving-the-opm-ddi"></a>OPM DDI の取得


次のシーケンスは、Microsoft DirectX graphics カーネルサブシステム (Dxgkrnl) がディスプレイミニポートドライバーの[OPM DDI](supporting-output-protection-manager.md)を取得する方法を示しています。

1. DirectX graphics カーネルサブシステムは、ディスプレイミニポートドライバーの[**DxgkDdiAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)関数を呼び出して、グラフィックスアダプターのコンテキストブロックを作成し、そのグラフィックスアダプターへのハンドルを返します。

2. DirectX graphics カーネルサブシステムは、次の表の値を使用して[**クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_query_interface)構造を初期化します。

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
   <td align="left"><p>sizeof (DXGK_OPM_INTERFACE)</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>バージョン</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>DXGK_OPM_INTERFACE_VERSION_1</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>Interface</strong></p></td>
   <td align="left"><p>PINTERFACE</p></td>
   <td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface" data-raw-source="[&lt;strong&gt;DXGK_OPM_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)"><strong>DXGK_OPM_INTERFACE</strong></a>構造体へのポインター</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceSpecificData</strong></p></td>
   <td align="left"><p>PVOID</p></td>
   <td align="left"><p>NULL</p></td>
   </tr>
   </tbody>
   </table>

     

3. DirectX graphics カーネルサブシステムは、表示ミニポートドライバーの[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数への呼び出しで、初期化されたクエリ\_インターフェイスを渡します。

4. ディスプレイミニポートドライバーで OPM インターフェイスがサポートされていない場合、 [**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)はサポートされて\_いない状態\_返す必要があります。

   ディスプレイミニポートドライバーで OPM がサポートされている場合、 [**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)は、 [**QUERY\_interface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_query_interface)の**インターフェイス**メンバーで受信した[**DXGK\_\_OPM インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)構造体を、値と共に初期化します。次の表を例に示します。

   **メンバー名、型、および値:**

   <span id="Size"></span><span id="size"></span><span id="SIZE"></span>**幅**  
   型 USHORT

   sizeof (DXGK\_OPM\_INTERFACE)

   <span id="Version"></span><span id="version"></span><span id="VERSION"></span>**バージョン**  
   型 USHORT

   DXGK\_OPM\_インターフェイス\_バージョン\_1

   <span id="InterfaceReference"></span><span id="interfacereference"></span><span id="INTERFACEREFERENCE"></span>**InterfaceReference**  
   型 PINTERFACE\_参照

   ディスプレイミニポートドライバーの**InterfaceReference**ルーチンへのポインター ( **InterfaceReference**の詳細については、[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造の「解説」セクションを参照してください)。

   <span id="InterfaceDereference"></span><span id="interfacedereference"></span><span id="INTERFACEDEREFERENCE"></span>**InterfaceDereference 参照**  
   型 PINTERFACE\_逆参照

   ディスプレイミニポートドライバーの**Interfacedereference 参照**ルーチンへのポインター ( **interfacedereference**参照の詳細については、[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造の「解説」を参照してください)。

   <span id="DxgkDdiOPMGetCertificateSize"></span><span id="dxgkddiopmgetcertificatesize"></span><span id="DXGKDDIOPMGETCERTIFICATESIZE"></span>**DxgkDdiOPMGetCertificateSize**  
   「DXGKDDI\_OPM\_\_証明書の\_サイズを取得する」と入力します。

   ディスプレイミニポートドライバーの[**DxgkDdiOPMGetCertificateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)関数へのポインター

   <span id="DxgkDdiOPMGetCertificate"></span><span id="dxgkddiopmgetcertificate"></span><span id="DXGKDDIOPMGETCERTIFICATE"></span>**DxgkDdiOPMGetCertificate**  
   「DXGKDDI\_OPM\_\_証明書を取得する」と入力します。

   ディスプレイミニポートドライバーの[**DxgkDdiOPMGetCertificate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)関数へのポインター

   <span id="DxgkDdiOPMCreateProtectedOutput"></span><span id="dxgkddiopmcreateprotectedoutput"></span><span id="DXGKDDIOPMCREATEPROTECTEDOUTPUT"></span>**DxgkDdiOPMCreateProtectedOutput**  
   「DXGKDDI\_OPM\_作成\_保護された\_出力

   ディスプレイミニポートドライバーの[**DxgkDdiOPMCreateProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)関数へのポインター

   <span id="DxgkDdiOPMGetRandomNumber"></span><span id="dxgkddiopmgetrandomnumber"></span><span id="DXGKDDIOPMGETRANDOMNUMBER"></span>**DxgkDdiOPMGetRandomNumber**  
   「DXGKDDI\_OPM\_\_ランダム\_番号を取得する」と入力します。

   ディスプレイミニポートドライバーの[**DxgkDdiOPMGetRandomNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)関数へのポインター

   <span id="DxgkDdiOPMSetSigningKeyAndSequenceNumbers"></span><span id="dxgkddiopmsetsigningkeyandsequencenumbers"></span><span id="DXGKDDIOPMSETSIGNINGKEYANDSEQUENCENUMBERS"></span>**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**  
   DXGKDDI\_OPM\_\_署名\_キー\_および\_シーケンス\_番号を設定します。

   ディスプレイミニポートドライバーの[**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)関数へのポインター

   <span id="DxgkDdiOPMGetInformation"></span><span id="dxgkddiopmgetinformation"></span><span id="DXGKDDIOPMGETINFORMATION"></span>**DxgkDdiOPMGetInformation**  
   DXGKDDI\_OPM\_\_情報の取得

   ディスプレイミニポートドライバーの[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)関数へのポインター

   <span id="DxgkDdiOPMGetCOPPCompatibleInformation"></span><span id="dxgkddiopmgetcoppcompatibleinformation"></span><span id="DXGKDDIOPMGETCOPPCOMPATIBLEINFORMATION"></span>**DxgkDdiOPMGetCOPPCompatibleInformation**  
   DXGKDDI\_OPM\_\_COPP\_互換性のある\_情報

   ディスプレイミニポートドライバーの[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)関数へのポインター

   <span id="DxgkDdiOPMConfigureProtectedOutput"></span><span id="dxgkddiopmconfigureprotectedoutput"></span><span id="DXGKDDIOPMCONFIGUREPROTECTEDOUTPUT"></span>**DxgkDdiOPMConfigureProtectedOutput**  
   DXGKDDI\_OPM\_\_保護された\_出力の構成

   ディスプレイミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数へのポインター

   <span id="DxgkDdiOPMDestroyProtectedOutput"></span><span id="dxgkddiopmdestroyprotectedoutput"></span><span id="DXGKDDIOPMDESTROYPROTECTEDOUTPUT"></span>**DxgkDdiOPMDestroyProtectedOutput**  
   DXGKDDI\_OPM\_破棄\_保護された\_出力

   ディスプレイミニポートドライバーの[**DxgkDdiOPMDestroyProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)関数へのポインター

5. OPM インターフェイスを使用してディスプレイミニポートドライバーを終了すると、ドライバーはその**Interfacedereference 参照**ルーチンを呼び出します。 ドライバーは、 [**DxgkDdiRemoveDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)関数が呼び出される前に、 **interfacedereference 参照**を呼び出す必要があります。

 

 





