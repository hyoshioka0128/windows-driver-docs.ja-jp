---
title: WDI RX パス
description: このセクションでは、WDI RX パスについて説明します。
ms.assetid: EEEA7181-4A24-4F40-8A44-65EC38D1A867
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23dd4df927de8e5e2d4007f107c53749830bde53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842894"
---
# <a name="wdi-rx-path"></a>WDI RX パス


## <a name="rx-path-components"></a>RX パスのコンポーネント


次の図は、RX パスコンポーネントを示しています。

![wdi 受信パス](images/wdi-receive-path-block-diagram.png)

## <a name="rx-manager-rxmgr"></a>RX マネージャー (RxMgr)


RX マネージャーは、ターゲットにオフロードされない、または RxEngine によって実行される、受信処理のステップを実行します。

| RX 関数            | 説明                                                                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MSDU 破棄           | エラーのある MSDUs を破棄します。                                                                                                                                                                      |
| キューと調整 | Dpc ウォッチドッグを管理して、DPC ごとの数が多すぎることや、ディスパッチレベルでは長すぎることからバグチェックが行われないようにします。 調整に役立つように、必要に応じて RxEngine にバック圧力を提供します。 |

 

## <a name="rxengine"></a>RxEngine


RxEngine は、ターゲットとの間でデータ同期メッセージを送受信し、RX 記述子の形式を解釈し、直接のハードウェアのバッファーをソフトウェア RX DMAs に管理します。

| RX 関数                             | 説明                                                                                                                                                                                                                                              |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ホストからターゲットへのメッセージの構築     | ホストからターゲットへのデータパスに関連するメッセージを構築します。                                                                                                                                                                                                     |
| ターゲットからホストへのメッセージ解析          | [*NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)などのターゲットからホストへのデータ同期メッセージを解析し、処理します。                                                                                                          |
| ターゲット RX 記述子の解釈 | ターゲット固有の記述子から RX フレームの属性を照会するためのインターフェイス (関数) を提供します。                                                                                                                                                   |
| RX FIFO 管理                      | ターゲットがいっぱいになるように空の RX バッファーをポストするために、ターゲットとしてアクセスできる FIFO を指定します。 [*NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)処理中に FIFO からバッファーを削除し、置換された空のバッファーを提供します。 |
| RX バッファープールの管理               | 受信フレームの DMA 転送用のバッファープールを保持します。                                                                                                                                                                                           |
| MPDU 破棄                            | MPDUs をエラーと共に破棄します。 ターゲットは、"破棄" とマークされた受信フレームを示します。たとえば、FCS エラーや ARQ 重複エラーが原因です。 これは、ターゲットによって実装されていない場合にのみ実行されます。                                              |
| MPDU の順序変更                            | MPDUs が到着する前に、その前に存在しない MPDUs が到着するまで、配列の順序を並べ替えることができます。 これは、ターゲットによって実装されていない場合にのみ実行されます。                                                                                                   |
| MPDU PN chk                             | これは、ターゲットにオフロードされていない場合にのみ実行されます。                                                                                                                                                                                                  |
| MSDU フラグメントの再構築                | これは、ターゲットにオフロードされていない場合にのみ実行されます。                                                                                                                                                                                                  |

 

## <a name="rx-path-requests-and-indications"></a>RX パスの要求とインジケーター


RX パスの要求と参照関数のリファレンスについては、「 [WDI RX Path Functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

## <a name="related-topics"></a>関連トピック


[*NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)

[WDI RX パス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






