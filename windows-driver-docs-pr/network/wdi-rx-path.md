---
title: WDI RX パス
description: このセクションには、WDI RX パスがについて説明します
ms.assetid: EEEA7181-4A24-4F40-8A44-65EC38D1A867
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa477567ccf32c0c83f394b20ce5c4a1d7a10b7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384338"
---
# <a name="wdi-rx-path"></a>WDI RX パス


## <a name="rx-path-components"></a>RX のパス コンポーネント


次の図は、RX のパス コンポーネントを示しています。

![wdi 受信パス](images/wdi-receive-path-block-diagram.png)

## <a name="rx-manager-rxmgr"></a>RX マネージャー (RxMgr)


RX マネージャーは、実行、ターゲットにオフロードまたは、RxEngine によって実行されていない処理手順が表示されます。

| RX 関数            | 説明                                                                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MSDU 破棄           | エラーのある MSDUs を破棄します。                                                                                                                                                                      |
| キューと調整 | ディスパッチ レベルが多すぎますがない、DPC ごと、および長すぎるからでバグチェックを防ぐために、DPC ウォッチドッグを管理します。 調整を支援する適切な場合に RxEngine に背圧を提供します。 |

 

## <a name="rxengine"></a>RxEngine


RxEngine で、送信とターゲットの間のデータ同期メッセージを受信および RX 記述子の形式を解釈、およびソフトウェア RX Dma を直接ハードウェアのバッファーを管理します。

| RX 関数                             | 説明                                                                                                                                                                                                                                              |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ターゲットへのホストのメッセージの構築     | ホストとターゲットのデータ パスに関連するメッセージを構築します。                                                                                                                                                                                                     |
| ターゲットからホストへのメッセージの解析          | 解析し、ターゲットのホストへのデータ同期メッセージの処理をなど[ *NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)します。                                                                                                          |
| ターゲット RX 記述子の解釈 | ターゲット固有の記述子から RX フレームの属性を照会するためのインターフェイス (関数) を提供します。                                                                                                                                                   |
| RX の FIFO の管理                      | ターゲット入力を空の RX バッファーをポストするためには、ターゲットにアクセス可能な FIFO を提供します。 バッファーを削除中に、FIFO から[ *NdisWdiRxInorderDataIndication* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)処理、および置換の空のバッファーを提供します。 |
| RX のバッファー プールの管理               | 受信のフレームの DMA 転送用のバッファーのプールを維持します。                                                                                                                                                                                           |
| MPDU 破棄                            | エラーのある MPDUs を破棄します。 ターゲットでは、受信フレームが破棄 for - たとえば、FCS エラーまたは ARQ 重複エラーのためにマークされていることを示します。 これは、しないターゲットによって実装されている場合のみ行います。                                              |
| MPDU 並べ替え                            | 不足している前 MPDUs が到着するまでは、RX 並べ替え配列内の順序で MPDUs を格納します。 これは、しないターゲットによって実装されている場合のみ行います。                                                                                                   |
| MPDU PN から chk                             | ターゲットに、オフロードしない場合は、これはのみです。                                                                                                                                                                                                  |
| MSDU フラグメントの再構築                | ターゲットに、オフロードしない場合は、これはのみです。                                                                                                                                                                                                  |

 

## <a name="rx-path-requests-and-indications"></a>RX のパスの要求と表示


RX のパスの要求とを示す値関数のリファレンスを参照してください。 [WDI RX パス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

## <a name="related-topics"></a>関連トピック


[*NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)

[WDI RX パス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

 

 






