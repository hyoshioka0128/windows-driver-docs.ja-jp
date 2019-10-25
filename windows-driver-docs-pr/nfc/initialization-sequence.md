---
title: 初期化シーケンス
description: 次の図は、初期化中に NFC CX と NFCC によって交換される NCI パケットの高レベルセットを示しています。
ms.assetid: 4977E1D4-2546-4573-B555-FA87DB8A2168
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4433e99906369e310c978be4f9214d1ec023bbf4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838033"
---
# <a name="initialization-sequence"></a>初期化シーケンス


次の図は、初期化中に NFC CX と NFCC によって交換される NCI パケットの高レベルセットを示しています。 初期化を開始する前に、NFC CX ドライバーは、クライアントドライバーのプリ初期化シーケンスハンドラーが登録されている場合、それを呼び出します。 StateInit は、NCI reset、NCI initialization、standard NCI configuration of parameters、RF Interface and RF Protocol mapping という上位レベルのシーケンスで構成されています。 NFC クライアントドライバーは、初期化中に使用される一部の NCI 構成パラメーターの既定値を設定できます。これは、 [**NfcCxSetRfDiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)や[**Nfccxsetllcpconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetllcpconfig)などの nfc CX インターフェイス関数によって行われます。 初期化の完了後、初期化完了シーケンスハンドラーが呼び出されます。 初期化が完了した後の次の状態は、StateRfIdle です。

![初期化シーケンス](images/initializationsequence.png)

NFCC が適切に機能するための重要な要件の1つは、NFC クライアントドライバーからのファームウェアのダウンロード操作を処理することです。 NFC CX の設計は、コントローラーにファームウェアをダウンロードするための複数の異なる設計をサポートするのに十分な柔軟性を備えています。

ファームウェアのダウンロードが必要かどうかを判断するには、一部のチップセットでファームウェアのバージョン管理情報の NCI を初期化する必要があります。 このような設計では、ファームウェアのダウンロードを実現するための NFC CX および NFC クライアントドライバーのステートマシンが次のように表示されます。 青い状態は NFC CX によって指定された状態に対応し、灰色の状態は NFC クライアントドライバーの状態に対応します。 NCI の初期化後、つまり、初期化完了シーケンスハンドラーでは、クライアントドライバーはコア\_INIT\_RSP メッセージの現在のバージョンを確認し、ファームウェアのダウンロード操作が必要かどうかを判断します。 "No" の場合、NFC CX ドライバーの通常の状態遷移は引き続き次の状態になります。 [はい] の場合、クライアントドライバーは NFC CX に再起動を要求します。 シャットダウンが完了すると、NFC クライアントドライバーはファームウェアのダウンロードを実装できます。

![ファームウェアのダウンロード後の初期化](images/initializationsequence1.png)

一部の NFCC ファームウェア実装には、ファームウェアのダウンロードが必要かどうかを判断するために、NCI のコンテキストの外部で帯域外メカニズムが用意されています。 このような場合、事前初期化シーケンスを処理するときに、NFC クライアントドライバーは、そのコネクタの状態を実装して、ファームウェアのダウンロードが必要かどうかを判断できます。 [はい] を選択すると、ファームウェアのダウンロード操作がクライアントドライバーによって実行されます。 ファームウェアのダウンロードが不要な場合は、次の状態への通常の動作が続行されます。 次の図は、ファームウェアのダウンロード NCI 初期化のステートマシン処理を示しています。

![ファームウェアのダウンロードの事前初期化](images/firmwaredownloadpreinitialization.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

