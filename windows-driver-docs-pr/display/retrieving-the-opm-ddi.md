---
title: OPM DDI を取得します。
description: OPM DDI を取得します。
ms.assetid: 84218245-f5f3-4a6f-88ed-9cd5db224e30
keywords:
- OPM WDK の表示、DDI を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b178d08fc6616c6b81d860a97e8587f0bf600347
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536283"
---
# <a name="retrieving-the-opm-ddi"></a>OPM DDI を取得します。


次の順序は、Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) を表示ミニポート ドライバーを取得する方法を示しています[OPM DDI](supporting-output-protection-manager.md):。

1. DirectX グラフィックスのカーネル サブシステム呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiAddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff559586)グラフィックス アダプターのコンテキストのブロックを作成して、そのグラフィックス アダプターにハンドルを返す関数。

2. DirectX グラフィックスのカーネルのサブシステムを初期化します、 [**クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff569225)次の表の値を持つ構造体。

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
   <td align="left"><p><strong>インターフェイス</strong></p></td>
   <td align="left"><p>PINTERFACE</p></td>
   <td align="left"><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff561986" data-raw-source="[&lt;strong&gt;DXGK_OPM_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561986)"> <strong>DXGK_OPM_INTERFACE</strong> </a>構造体</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceSpecificData</strong></p></td>
   <td align="left"><p>PVOID</p></td>
   <td align="left"><p>NULL</p></td>
   </tr>
   </tbody>
   </table>

     

3. DirectX グラフィックスのカーネル サブシステムが初期化されたクエリを渡す\_ディスプレイ ミニポート ドライバーの呼び出しでインターフェイス[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)関数。

4. ディスプレイのミニポート ドライバーが、OPM インターフェイスをサポートしていない場合[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)状態を返す必要があります\_いない\_サポートされています。

   ディスプレイのミニポート ドライバー OPM をサポートしている場合[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)を初期化します、 [ **DXGK\_OPM\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff561986)で受信した構造体、**インターフェイス**のメンバー [**クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff569225)で値を持つ、次の表にします。

   **メンバーの名前、種類、および値:**

   <span id="Size"></span><span id="size"></span><span id="SIZE"></span>**サイズ**  
   USHORT 型

   sizeof (DXGK\_OPM\_インターフェイス)

   <span id="Version"></span><span id="version"></span><span id="VERSION"></span>**バージョン**  
   USHORT 型

   DXGK\_OPM\_インターフェイス\_バージョン\_1

   <span id="InterfaceReference"></span><span id="interfacereference"></span><span id="INTERFACEREFERENCE"></span>**InterfaceReference**  
   入力 PINTERFACE\_リファレンス

   ディスプレイのミニポート ドライバーへのポインター **InterfaceReference**ルーチン (について**InterfaceReference**の「解説」を参照してください、 [**インターフェイス** ](https://msdn.microsoft.com/library/windows/hardware/ff547825)構造です)。

   <span id="InterfaceDereference"></span><span id="interfacedereference"></span><span id="INTERFACEDEREFERENCE"></span>**InterfaceDereference**  
   入力 PINTERFACE\_逆参照

   ディスプレイのミニポート ドライバーへのポインター **InterfaceDereference**ルーチン (について**InterfaceDereference**の「解説」を参照してください、 [**インターフェイス** ](https://msdn.microsoft.com/library/windows/hardware/ff547825)構造です)。

   <span id="DxgkDdiOPMGetCertificateSize"></span><span id="dxgkddiopmgetcertificatesize"></span><span id="DXGKDDIOPMGETCERTIFICATESIZE"></span>**DxgkDdiOPMGetCertificateSize**  
   入力 DXGKDDI\_OPM\_取得\_証明書\_サイズ

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetCertificateSize** ](https://msdn.microsoft.com/library/windows/hardware/ff559715)関数

   <span id="DxgkDdiOPMGetCertificate"></span><span id="dxgkddiopmgetcertificate"></span><span id="DXGKDDIOPMGETCERTIFICATE"></span>**DxgkDdiOPMGetCertificate**  
   入力 DXGKDDI\_OPM\_取得\_証明書

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetCertificate** ](https://msdn.microsoft.com/library/windows/hardware/ff559711)関数

   <span id="DxgkDdiOPMCreateProtectedOutput"></span><span id="dxgkddiopmcreateprotectedoutput"></span><span id="DXGKDDIOPMCREATEPROTECTEDOUTPUT"></span>**DxgkDdiOPMCreateProtectedOutput**  
   入力 DXGKDDI\_OPM\_作成\_PROTECTED\_出力

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMCreateProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559705)関数

   <span id="DxgkDdiOPMGetRandomNumber"></span><span id="dxgkddiopmgetrandomnumber"></span><span id="DXGKDDIOPMGETRANDOMNUMBER"></span>**DxgkDdiOPMGetRandomNumber**  
   入力 DXGKDDI\_OPM\_取得\_ランダム\_数

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetRandomNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff559730)関数

   <span id="DxgkDdiOPMSetSigningKeyAndSequenceNumbers"></span><span id="dxgkddiopmsetsigningkeyandsequencenumbers"></span><span id="DXGKDDIOPMSETSIGNINGKEYANDSEQUENCENUMBERS"></span>**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**  
   DXGKDDI\_OPM\_設定\_署名\_キー\_AND\_シーケンス\_番号

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMSetSigningKeyAndSequenceNumbers** ](https://msdn.microsoft.com/library/windows/hardware/ff559735)関数

   <span id="DxgkDdiOPMGetInformation"></span><span id="dxgkddiopmgetinformation"></span><span id="DXGKDDIOPMGETINFORMATION"></span>**DxgkDdiOPMGetInformation**  
   DXGKDDI\_OPM\_取得\_情報

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)関数

   <span id="DxgkDdiOPMGetCOPPCompatibleInformation"></span><span id="dxgkddiopmgetcoppcompatibleinformation"></span><span id="DXGKDDIOPMGETCOPPCOMPATIBLEINFORMATION"></span>**DxgkDdiOPMGetCOPPCompatibleInformation**  
   DXGKDDI\_OPM\_取得\_COPP\_互換性のある\_情報

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)関数

   <span id="DxgkDdiOPMConfigureProtectedOutput"></span><span id="dxgkddiopmconfigureprotectedoutput"></span><span id="DXGKDDIOPMCONFIGUREPROTECTEDOUTPUT"></span>**DxgkDdiOPMConfigureProtectedOutput**  
   DXGKDDI\_OPM\_構成\_PROTECTED\_出力

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)関数

   <span id="DxgkDdiOPMDestroyProtectedOutput"></span><span id="dxgkddiopmdestroyprotectedoutput"></span><span id="DXGKDDIOPMDESTROYPROTECTEDOUTPUT"></span>**DxgkDdiOPMDestroyProtectedOutput**  
   DXGKDDI\_OPM\_破棄\_PROTECTED\_出力

   ディスプレイのミニポート ドライバーへのポインター [ **DxgkDdiOPMDestroyProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559708)関数

5. ディスプレイのミニポート ドライバーが完了すると、ドライバーの呼び出しである OPM インターフェイスを使用してその**InterfaceDereference**ルーチン。 ドライバーを呼び出す必要があります**InterfaceDereference**する前にその[ **DxgkDdiRemoveDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff559789)関数が呼び出されます。

 

 





