---
title: OPM DDI の使用
description: OPM DDI の使用
ms.assetid: cd3c78a4-0241-48ab-9005-c544db199eb5
keywords:
- DDI について、OPM WDK の表示
- OPM WDK の表示、作成、保護された出力します。
- OPM WDK の表示、保護された破棄の出力します。
- 証明書の取得、OPM WDK の表示
- OPM WDK の表示、保護されている出力の構成
- OPM WDK の表示、保護を取得する情報を出力します。
- アダプターの情報を取得するには、グラフィックス、OPM WDK の表示
- 保護レベルを変更する、WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 075b9140c82d314dd60f18ed99e0b56809b304f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579055"
---
# <a name="using-the-opm-ddi"></a>OPM DDI の使用


Microsoft DirectX グラフィックスのカーネル サブシステム (*Dxgkrnl.sys*) 使用 OPM DDI OPM を作成するには、出力が保護されている、OPM 保護されている出力の破棄、証明書の取得、保護された出力を構成、情報を取得する約保護出力、およびグラフィックス アダプターに関する情報を取得します。 DirectX グラフィックスのカーネル サブシステムは、ディスプレイのミニポート ドライバーを呼び出すときに OPM DDI 関数にポインターを取得[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)識別されるインターフェイスを照会する関数GUID による\_DEVINTERFACE\_OPM と DXGK\_OPM\_インターフェイス\_バージョン\_1。 次のシーケンスでは、OPM DDI が通常作成、操作、および保護されている OPM 出力を破棄する使用方法について説明します。

1.  DirectX グラフィックスのカーネル サブシステムの呼び出し、 [ **DxgkDdiOPMCreateProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559705) OPM を作成する関数は、出力を保護します。 保護されている OPM 出力は、常に正確に 1 つの物理的なビデオ出力に対応します。 *DxgkDdiOPMCreateProtectedOutput*ハンドルを新しく作成された出力に返します。

2.  DirectX グラフィックスのカーネル サブシステムの呼び出し、 [ **DxgkDdiOPMGetCertificateSize** ](https://msdn.microsoft.com/library/windows/hardware/ff559715)と[ **DxgkDdiOPMGetCertificate** ](https://msdn.microsoft.com/library/windows/hardware/ff559711)ディスプレイのミニポート ドライバーの OPM 証明書または COPP 証明書とそのサイズを取得する関数。
    **注**  *DxgkDdiOPMCreateProtectedOutput*、 *DxgkDdiOPMGetCertificateSize*、および*DxgkDdiOPMGetCertificate*される唯一の OPM DDI 関数にはDirectX グラフィックスのカーネルのサブシステムでは、保護された出力を識別するハンドルは渡されません。

     

3.  DirectX グラフィックスのカーネル サブシステムの呼び出し、 [ **DxgkDdiOPMGetRandomNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff559730)保護されている出力の乱数を取得します。

4.  DirectX グラフィックスのカーネル サブシステムへの呼び出しで 256 バイト バッファーを渡す、 [ **DxgkDdiOPMSetSigningKeyAndSequenceNumbers** ](https://msdn.microsoft.com/library/windows/hardware/ff559735)関数。 バッファーには、ディスプレイのミニポート ドライバーの公開キーのいずれかで暗号化されたデータが含まれています。 公開キーの詳細については、ダウンロード、出力コンテンツの保護に関するドキュメントから、[出力 Content Protection と Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc) web サイト。 使用される公開キーは、保護されている出力のセマンティクスに依存します。 ディスプレイのミニポート ドライバーの OPM 証明書の公開キーは、保護されている出力が OPM セマンティクスを持つ場合に使用されます。 ディスプレイのミニポート ドライバーの COPP 証明書の公開キーは、保護されている出力が COPP セマンティクスを持つ場合に使用されます。 データの暗号化に使用される暗号化スキームは、保護されている出力のセマンティクスも異なります。 データには、保護されている出力が OPM セマンティクス標準の RSA アルゴリズムの場合は、保護されている出力がある COPP セマンティクスと RSAES OAEP 暗号化スキームが暗号化されます。 RSA、AES、および RSAES OAEP については、次を参照してください。、 [RSA Laboratories](https://go.microsoft.com/fwlink/p/?linkid=70411) web サイト。 ディスプレイのミニポート ドライバーでは、適切な秘密キーと復号化メソッドを使用して、データの暗号化を解除します。 ランダムな番号、2 つのランダム シーケンス番号、および 128 ビットの AES キーが復号化されたデータです。 表示ミニポート ドライブは、ランダムな数値が、ドライバーが返すときに、ランダムな数字と一致することにより、その[ **DxgkDdiOPMGetRandomNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff559730)関数が呼び出されました。 ドライバーは、2 つのシーケンス番号と 128 ビット AES キーを格納します。

5.  DirectX グラフィックスのカーネルのサブシステムを呼び出すようになりましたことができます、 [ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)または[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)保護されている出力から情報を取得する関数。 DirectX グラフィックスのカーネルのサブシステムを呼び出すことも[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)保護された出力を構成します。 *DxgkDdiOPMGetInformation*出力に OPM セマンティクスがある場合にのみ呼び出すことができますと*DxgkDdiOPMGetCOPPCompatibleInformation*出力に COPP セマンティクスがある場合にのみ呼び出すことができます。 DirectX グラフィックス カーネル サブシステム呼び出し通常、 *DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*出力とし、呼び出し情報を取得する*DxgkDdiOPMConfigureProtectedOutput*出力を構成する 1 つ以上の時間。 次に、DirectX グラフィックスのカーネルのサブシステムを呼び出す*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*もう一度です。 DirectX グラフィックスのカーネル サブシステムは呼び出すことで、次の種類の情報を取得することができます*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*:

    -   出力のコネクタの種類。
    -   出力をサポートするコンテンツの保護の種類。 出力は、アナログ コピー防止 (ACP) をサポートできる現在[コンテンツ生成管理システム アナログ (CGMS A)](cgms-a-standards.md)、高帯域幅デジタル コンテンツの保護 (HDCP)、およびディスプレイ ポート等コンテンツ保護 (DPCP)。 ACP の詳細については、次を参照してください。、 [Rovi (旧称 Macrovision)](https://go.microsoft.com/fwlink/p/?linkid=71273) web サイト。 HDCP の詳細については、、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)を参照してください。 ディスプレイ ポート等の詳細については、次を参照してください。、[ディスプレイ ポート等](https://go.microsoft.com/fwlink/p/?linkid=71382)Web 記事。
    -   特定の保護の種類の現在仮想保護レベルを出力の。
    -   特定の保護の種類の物理的な出力の実際の保護レベル。
    -   バージョンの HDCP システム Renewability メッセージ (SRM)、出力は現在使用されています。 HDCP SRM の詳細については、、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)を参照してください。 のみ[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)この情報を取得できます。
    -   接続されている HDCP デバイスのキーの選択のベクトル (KSV) と HDCP デバイスは、repeater、かどうか。 のみ[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)この情報を取得できます。 HDCP リピータと KSVs の詳細については、、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)を参照してください。
    -   グラフィックス アダプターを使用して拡張バスの種類。 PCI、AGP 拡張バスの例に示します。
    -   モニターに保護された出力に関連付けられている物理コネクタから送信されるイメージの形式です。
    -   CGMS A ACP シグナリング標準であり、保護された出力をサポートしているとします。 のみ[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)この情報を取得できます。
    -   出力の識別子です。
    -   電気の特性のデジタル ビデオ インターフェイス (DVI) は、コネクタを出力します。

    DirectX グラフィックスのカーネル サブシステムは呼び出すことで、次の設定を変更することができます[ **DxgkDdiOPMConfigureProtectedOutput**](https://msdn.microsoft.com/library/windows/hardware/ff559701):

    -   出力の保護の種類のいずれかの現在の保護レベル。 たとえば、 *DxgkDdiOPMConfigureProtectedOutput*できます有効または無効に HDCP とできます ACP の保護を無効に現在の ACP 保護レベルを変更します。
    -   保護された出力を使用して現在 HDCP SRM します。
    -   保護された出力を使用する現在のシグナリング標準。 この変更は、出力に COPP セマンティクスがある場合にのみ実行できます。

6.  DirectX グラフィックスのカーネル サブシステム呼び出し[ **DxgkDdiOPMDestroyProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559708)それが終了したら、保護されている出力オブジェクトを使用します。

 

 





